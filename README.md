Aqui está a estrutura do README.md completamente ajustada e formatada para o seu repositório Sysmon-monitor-ultra-leve-cpu, incluindo o link oficial do projeto, instruções claras de clone e instalação:

📄 Conteúdo para o seu README.md
Markdown

# Sysmon - Monitor de Sistema Ultra Leve

O **Sysmon** é um monitor de sistema TUI (Terminal User Interface) extremamente leve, desenvolvido em Bash puro para distribuições Linux. Projetado para oferecer baixo consumo de memória (~8 MB RAM) sem requerer dependências pesadas de ambientes gráficos (Qt/GTK) ou uso de GPU.

---

## 🌟 Principais Recursos

- **Detecção Automática de Hardware:** Identifica modelo da CPU, GPU (via `pci.ids` ou nome do driver) e informações DMI da máquina.
- **Monitoramento Térmico Automático:** Leitura direta de sensores `hwmon` (`temp*_max` e `temp*_crit`). Exibe alertas visuais (⚠) ao atingir limites críticos.
- **Arquivo de Configuração Simples:** Edição rápida em `~/.config/sysmon/sysmon.conf` pressionando a tecla `e` durante a execução.
- **Lançador de Terminal Universal:** Abre automaticamente no emulador de terminal disponível no sistema e cria atalho no menu de aplicações.
- **Interface Otimizada:** Exibição condicional de quadros (esconde bateria em desktops, zram ou GPUs sem dados).

---

## 🚀 Instalação Rápida

### Opção 1: Via Git (Recomendado)

```bash
git clone [https://github.com/TsukiAkira/Sysmon-monitor-ultra-leve-cpu.git](https://github.com/TsukiAkira/Sysmon-monitor-ultra-leve-cpu.git)
cd Sysmon-monitor-ultra-leve-cpu
./install.sh

Opção 2: Instalação Global (Todos os usuários)
Bash

sudo PREFIX=/usr/local ./install.sh

⌨️ Atalhos de Teclado
TeclaAçãoeAbre o arquivo de configuração no editor padrão ($EDITOR, nano ou vi) e recarrega ao fechar.xFinaliza processos selecionados.PgUp / PgDnNavegação nas listas e tabelas.qSai da aplicação.
⚙️ Personalização (sysmon.conf)
O arquivo de configuração é criado automaticamente em ~/.config/sysmon/sysmon.conf. Exemplo de ajustes manuais:

Ini, TOML

# Renomear rótulos de sensores
label.nvme = SSD

# Definir limites térmicos personalizados (°C)
limit.CPU = 90
limit.GPU = 95
limit.NVMe = 82.8

🗑️ Desinstalação
Para remover o Sysmon do sistema:

Bash

./uninstall.sh

Se tiver instalado globalmente:

Bash

sudo PREFIX=/usr/local ./uninstall.sh

📄 Licença
Distribuído sob a licença MIT. Veja o arquivo LICENSE para mais detalhes.

---

### 📌 Passos para atualizar no repositório local:

1. Abra o arquivo `README.md` no seu projeto e substitua o texto pelo bloco acima.
2. No terminal, execute os comandos para enviar a atualização para o GitHub:

```bash
git add README.md
git commit -m "docs: atualiza README com informacoes completas e links de clone"
git push origin main
