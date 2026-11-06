tem instalado ? 
remmova :


#!/bin/bash

echo "🔍 Verificando se o DWService já está instalado..."

# Verifica se o diretório de instalação existe
if [ -d "/usr/share/dwagent" ] || [ -d "/usr/local/dwagent" ]; then
    echo "⚠️ DWService já está instalado. Removendo instalação antiga..."
    
    # Para o serviço se estiver rodando
    systemctl stop dwagent.service 2>/dev/null
    
    # Remove o serviço do systemd
    systemctl disable dwagent.service 2>/dev/null
    
    # Remove diretórios antigos
    rm -rf /usr/share/dwagent /usr/local/dwagent
    
    # Remove scripts de inicialização
    rm -f /etc/systemd/system/dwagent.service /etc/init.d/dwagent
    
    echo "🧹 Instalação antiga removida com sucesso!"
fi

# Baixa o script de instalação do DWAgent
echo "🔽 Baixando agente DWService..."
wget -q https://www.dwservice.net/download/dwagent.sh -O dwagent.sh

# Dá permissão de execução
echo "🔧 Dando permissão de execução..."
chmod +x dwagent.sh

# Executa o instalador
echo "🚀 Iniciando instalação..."
./dwagent.sh

# Limpa o instalador depois da execução
rm -f dwagent.sh

echo "✅ Instalação concluída!"
