# cryo-sysmon

Monitor de sistema **TUI** (estilo htop) em **bash puro**, sem dependências extras, para qualquer Linux.
Mostra CPU, GPU, RAM, temperaturas, bateria e processos, com tema truecolor "CRYO CORE".

*English: a lightweight pure-bash terminal system monitor for Linux (CPU, GPU, RAM, temperatures, battery, processes). Reads sysfs/procfs directly, no external dependencies.*

<!-- Coloque aqui um print: docs/screenshot.png
![screenshot](docs/screenshot.png)
-->

## Recursos
- **Nomes do hardware detectados sozinhos:** CPU, GPU (via `pci.ids`) e modelo da máquina (DMI).
- **Limites térmicos do próprio PC:** lê `temp*_max` e `temp*_crit` de cada sensor (hwmon), com padrões de reserva. Acima do limite crítico aparece ⚠.
- **Textos e limites editáveis:** tecla `e` abre a configuração no seu editor e recarrega ao fechar.
- **Matar processo:** `x` (ou Delete) pede confirmação: `t` = TERM, `k` = KILL.
- **Leve:** CPU% por delta (sem `sleep`), lista de processos com 1 `cat` + 1 `awk`, RAM por `/proc/meminfo`, quadro montado em memória e escrito com um único `printf`. Medido na máquina do autor: ~8 MB de RSS.
- **Adapta-se ao PC:** esconde quadros que não existem (bateria em desktop, zram, GPU sem dados).

## Requisitos
- Linux com `/proc` e `/sys`; **bash 5.0+** (usa `EPOCHREALTIME`); `awk` (gawk ou mawk) e `cat`.
- Terminal com **truecolor** e pelo menos **74 colunas**.
- GPU: AMD e Intel mostram uso/frequência quando o driver expõe no sysfs. **NVIDIA com driver proprietário não expõe esses dados**, então aparece `--`.
- A lista de "quem usa a GPU" usa `find -printf` (GNU findutils).

## Instalação
```sh
git clone https://github.com/SEU_USUARIO/cryo-sysmon.git
cd cryo-sysmon
./install.sh                          # só para o seu usuário (~/.local)
# ou, para todos:  sudo PREFIX=/usr/local ./install.sh
```
Depois procure **sysmon** no menu de aplicativos, ou rode `sysmon` no terminal
(se o comando não for encontrado, adicione `~/.local/bin` ao `PATH`).

Remover: `./uninstall.sh` (a configuração é mantida).

## Uso
```
sysmon            atualiza a cada 1 s
sysmon 0.5        intervalo em segundos (0.5 a 10)
sysmon --init     cria a configuração com exemplos
sysmon --conf     mostra o caminho da configuração
sysmon --ajuda    ajuda
```

| Tecla | Ação |
|---|---|
| `q` | sair |
| `↑` `↓` / `j` `k` | mover a seleção; `PgUp`/`PgDn` pulam 10 linhas |
| `s` | ordem dos processos: mem → cpu → pid |
| `x` / `Delete` | matar o processo selecionado (`t` = TERM, `k` = KILL, outra tecla cancela) |
| `e` | editar a configuração e recarregar |
| `+` / `-` | intervalo ±0,5 s |

PID 1 e o próprio sysmon são protegidos contra o kill.

## Configuração
Arquivo: `~/.config/sysmon/sysmon.conf` (formato `chave = valor`, `#` comenta, temperaturas em °C).

```ini
title        = MEU PC
cpu_name     = Meu processador
sensors_max  = 8
hide         = Core*,Sensor*,Tccd*
label.nvme   = SSD
limit.CPU    = 90
```
- `label.<chip>`: renomeia um sensor (`cat /sys/class/hwmon/*/name` lista os chips).
- `limit.<Texto exibido>`: define o limite do sensor.
- Outras chaves: `machine_name`, `gpu_name`, `subtitle`, `step`, `show_gpu`, `show_battery`, `gpu_bar`.

## Terminais
O launcher do menu usa o primeiro que encontrar: konsole, xfce4-terminal, xterm, lxterminal, mate-terminal,
gnome-terminal, foot, alacritty, kitty. Para forçar um: `SYSMON_TERMINAL=xterm sysmon-launch`.
No Konsole, `SYSMON_GEOMETRY_PX=700x986` define o tamanho da janela em pixels.

## Testes
```sh
bash tests/functest.sh     # compara as funções de desenho com a referência, byte a byte
```
A integração contínua (GitHub Actions) roda checagem de sintaxe, esse teste e um teste de fumaça em pty.

## Aviso sobre o nome
Já existe outro programa chamado "sysmon" (Sysinternals Sysmon para Linux). Este projeto instala o comando `sysmon`
em `~/.local/bin` por padrão; se você usa o outro, renomeie o arquivo ao instalar.

## Licença
MIT. Veja [LICENSE](LICENSE).
