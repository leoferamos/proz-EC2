# Configuração de Instância EC2 para a Banda de Miguel

A banda de Miguel te contratou para ajudá-los na criação de uma instância EC2 para organizar a documentação e os arquivos importantes da banda. Recentemente, a banda se interessou pelo mundo da computação em nuvem e decidiu explorar o Amazon EC2, um serviço popular de infraestrutura como serviço (IaaS) oferecido pela Amazon Web Services (AWS). Eles também conheceram o Amazon Linux, que é uma distribuição otimizada para a nuvem, sendo uma opção excelente para as instâncias EC2. Os membros da banda estão empolgados para testar essa tecnologia e começar a armazenar e gerenciar os seus documentos e arquivos na nuvem. Neste exercício, iremos ajudá-los com isso.

## Descrição
Este projeto documenta o processo de configuração de uma instância EC2 no Amazon Web Services (AWS), o anexo de um novo volume recém criado, a formatação de montagem do volume, a criação de arquivos no volume, e a verificação de saúde do volume.

## Passos Seguidos

### 1. Configuração da Instância EC2

1. **Acessar o Console da AWS**
   - Faça login no [Console da AWS](https://aws.amazon.com/console/).
   - No menu de serviços, navegue até EC2.

2. **Criar uma Nova Instância EC2**
   - Clique em "Launch Instance".
   - Escolha "Amazon Linux 2 AMI (HVM), SSD Volume Type".
   - Selecione o tipo de instância `t2.micro`.
   - Configure as opções de instância conforme necessário.
   - Adicione armazenamento conforme necessário (o padrão é 8 GB).
   - Configure o grupo de segurança para permitir SSH (porta 22).
   - Crie um novo par de chaves ou use um existente, fazendo download da chave privada.

### 2. Conexão via SSH

1. **Conectar à Instância EC2**
   - Abra o terminal do WSL2 e navegue até o local onde a chave privada foi salva

   - Conecte-se à instância EC2:

     ```sh
     ssh -i "ChaveAWSEC2.pem" ec2-user@<EC2-Public-IP>
     ```

     Substitua `<EC2-Public-IP>` pelo endereço IP público da sua instância.

### 3. Gerenciamento do Armazenamento

1. **Criar um Novo Volume EBS**
   - No console da AWS, vá para "Volumes" em "Elastic Block Store".
   - Clique em "Create Volume".
   - Configure o tamanho (por exemplo, 10 GB), a zona de disponibilidade (a mesma da sua instância EC2).
   - Clique em "Create Volume".

2. **Anexar o Volume à Instância EC2**
   - Selecione o volume recém-criado.
   - Clique em "Actions" -> "Attach Volume".
   - Escolha sua instância EC2 e especifique o dispositivo (por exemplo, `/dev/xvdf`).

### 4. Formatação e Montagem do Volume

1. **Formatar o Volume**
   - No terminal SSH conectado à instância, formate o volume:

     ```sh
     sudo mkfs -t ext4 /dev/xvdf
     ```

2. **Montar o Volume**
   - Crie um diretório para montar o volume:

     ```sh
     sudo mkdir /mnt/ebs
     ```

   - Monte o volume:

     ```sh
     sudo mount /dev/xvdf /mnt/ebs
     ```

   - Verifique se o volume está montado:

     ```sh
     df -h
     ```

### 5. Criação de Arquivos

1. **Criar um Arquivo de Texto**
   - Use um editor de texto (como `nano` ou `vi`) para criar um arquivo de texto:

     ```sh
     sudo nano /mnt/ebs/meuarquivo.txt
     ```

   - Adicione algum conteúdo ao arquivo, salve e saia.

### 6. Explorando Recursos

1. **Verificar o Status do Volume Montado**
   - Listar o conteúdo do diretório montado:

     ```sh
     ls -l /mnt/ebs
     ```

   - Verificar o espaço em disco disponível:

     ```sh
     df -h
     ```

   - Verificar o ponto de montagem:

     ```sh
     mount | grep /mnt/ebs
     ```

   - Verificar o conteúdo do arquivo criado:

     ```sh
     cat /mnt/ebs/meuarquivo.txt
     ```

### 7. Prints de Tela
(anexar prints)

### 8. Encerrando a Instância

Após a conclusão do exercício, a instância foi encerrada corretamente.



