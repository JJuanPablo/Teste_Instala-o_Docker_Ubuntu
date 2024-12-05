# Teste de Ambiente Docker

## Objetivo

Este teste visa verificar a instalação e configuração do Docker, criando um ambiente virtual baseado no Ubuntu e realizando um comando simples dentro de um container para garantir que o Docker está funcionando corretamente.

## Passos para Realizar o Teste

1. **Instalação do Docker**
   - Verifique se o Docker está instalado corretamente no seu sistema:
     ```bash
     docker --version
     ```

2. **Criando e Rodando o Container**
   - Crie um script chamado `teste_docker.sh` para automatizar o teste:
     ```bash
     nano teste_docker.sh
     ```

     O conteúdo do script será:

     ```bash
     #!/bin/bash

     echo "=== Teste de Ambiente Docker ==="

     # Verificar se o Docker está instalado
     if ! command -v docker &> /dev/null; then
         echo "Docker não encontrado. Por favor, instale o Docker antes de continuar."
         exit 1
     fi
     echo "Docker instalado. Versão: $(docker --version)"

     # Criar um container baseado no Ubuntu
     echo "Criando um container de teste baseado no Ubuntu..."
     docker run --name teste-ambiente-ubuntu -d ubuntu sleep infinity

     # Verificar se o container foi criado
     if [ "$(docker ps -q -f name=teste-ambiente-ubuntu)" ]; then
         echo "Container criado e rodando com sucesso!"
     else
         echo "Falha ao criar o container."
         exit 1
     fi

     # Testar o funcionamento do container
     echo "Executando um comando dentro do container..."
     docker exec teste-ambiente-ubuntu echo "O ambiente está funcionando!"

     # Limpar o ambiente (parar e remover o container)
     echo "Limpando o ambiente..."
     docker stop teste-ambiente-ubuntu > /dev/null
     docker rm teste-ambiente-ubuntu > /dev/null
     echo "Teste concluído e ambiente limpo."
     ```

3. **Tornando o Script Executável**
   - Após salvar o arquivo, torne o script executável:
     ```bash
     chmod +x teste_docker.sh
     ```

4. **Executando o Teste**
   - Execute o script:
     ```bash
     ./teste_docker.sh
     ```

5. **Resultado Esperado**
   - O script deve verificar se o Docker está instalado, criar e rodar o container Ubuntu com sucesso, executar o comando dentro do container e, em seguida, parar e remover o container, confirmando que o ambiente está funcionando corretamente.
