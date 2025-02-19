# Escola da Nuvem
Laboratórios desenvolvidos na Escola da Nuvem

## Laboratório 11 - Introdução ao Amazon EC2
Este laboratório fornece uma visão geral básica
 de como iniciar, redimensionar, gerenciar e monitorar uma instância do Amazon EC2.

### Overview 
![lab-scenario](https://github.com/user-attachments/assets/c80caea3-985d-44dc-94d2-9d0ba0013db6)


# O que é Amazon EC2?
é um serviço web que fornece capacidade de computação redimensionável na nuvem. Ele foi projetado para tornar a computação em nuvem em escala web mais fácil para desenvolvedores.
Amazon EC2 tem uma interface simples que permite que você obtenha e configure capacidade com o mínimo de atrito. Ela fornece a você controle completo dos seus recursos de computação e permite que você execute no ambiente de computação comprovado da Amazon. O Amazon EC2 reduz o tempo necessário para obter e inicializar de servidor para minutos, permitindo que você dimensione rapidamente a capacidade, tanto para cima quanto para baixo, conforme seus requisitos de computação mudam.

# Objetivos

- Inicie um servidor web com proteção de encerramento habilitada

- Monitore sua instância EC2

- Modifique o grupo de segurança que seu servidor web está usando para permitir acesso HTTP

- Redimensione sua instância do Amazon EC2 para dimensionar

- Proteção de término de teste

- Encerre sua instância EC2

## Tarefa 1: Iniciando sua instância EC2
Iniciará uma instância do Amazon EC2 com proteção de encerramento . A proteção de encerramento impede que você encerre acidentalmente uma instância do EC2. Você implantará sua instância com um script de Dados do Usuário que permitirá que você implante um servidor web simples.

- No AWS Management Console, no menu Serviços , escolha EC2 

- No painel de navegação esquerdo, escolha Painel do EC2 para garantir que você esteja na página do painel

- Selecione Iniciar instância e, em seguida, selecione Iniciar instância

## Etapa 1: nomeando sua instância EC2
Quando você nomeia sua instância, a AWS cria um par de valores-chave. A chave para esse par é Name , e o valor é o nome que você insere para sua instância EC2.

- No painel Nome e tags , na caixa de texto Nome , digite Web Server.

## Etapa 2: Escolhendo uma Amazon Machine Image (AMI)
Uma AMI fornece as informações necessárias para iniciar uma instância, que é um servidor virtual na nuvem. Uma AMI inclui o seguinte:

- Um modelo para o volume raiz da instância (por exemplo, um sistema operacional ou um servidor de aplicativos com aplicativos)

- Permissões de inicialização que controlam quais contas da AWS podem usar a AMI para iniciar instâncias

- Um mapeamento de dispositivo de bloco que especifica os volumes a serem anexados à instância quando ela é iniciada

A lista Quick Start contém as AMIs mais comumente usadas. Você também pode criar sua própria AMI ou selecionar uma AMI no AWS Marketplace, uma loja online onde você pode vender ou comprar software que roda na AWS.

- Localize o painel Imagens de aplicativos e sistemas operacionais (imagem de máquina da Amazon) .

- Em AMI Machine Image (AMI) , observe que a imagem AMI do Amazon Linux 2 é selecionada por padrão. Mantenha essa configuração.

## Etapa 3: Escolhendo um tipo de instância
O Amazon EC2 fornece uma ampla seleção de tipos de instância otimizados para se adequar a diferentes casos de uso. Os tipos de instância compreendem combinações variadas de CPU, memória, armazenamento e capacidade de rede e oferecem a flexibilidade de escolher a combinação apropriada de recursos para seus aplicativos. Cada tipo de instância inclui um ou mais tamanhos de instância para que você possa dimensionar seus recursos de acordo com os requisitos de sua carga de trabalho de destino.

- Selecione uma instância t3.micro . Este tipo de instância tem 2 CPUs virtuais e 1 GiB de memória.

- No menu suspenso, selecione t3.micro .

OBSERVAÇÃO : Você pode estar restrito ao uso de outros tipos de instância neste laboratório.

## Etapa 4: Configurando um par de chaves
O Amazon EC2 usa criptografia de chave pública para criptografar e descriptografar informações de login. Para fazer login na sua instância, você deve criar um par de chaves, especificar o nome do par de chaves ao iniciar a instância e fornecer a chave privada ao se conectar à instância.

- Neste laboratório, você não faz login na sua instância, portanto não precisa de um par de chaves.

- No painel Par de chaves (login) , selecione Continuar sem um par de chaves (não recomendado) .

## Etapa 5: Configurando as configurações de rede
Use este painel para configurar as configurações de rede.

O VPC indica em qual nuvem privada virtual (VPC) você quer iniciar a instância. Você pode ter vários VPCs, incluindo diferentes para desenvolvimento, teste e produção.

- No painel Configurações de rede , escolha Editar

- Para VPC - obrigatório , selecione Lab VPC .

- Ainda no painel Configurações de rede , configure o Grupo de segurança da seguinte forma:

- Nome do grupo de segurança - obrigatório :Web Server security group

- Descrição :Security group for my web server

Um grupo de segurança atua como um firewall virtual que controla o tráfego para uma ou mais instâncias. Ao iniciar uma instância, você associa um ou mais grupos de segurança à instância. Você adiciona regras a cada grupo de segurança que permitem tráfego de ou para suas instâncias associadas. Você pode modificar as regras para um grupo de segurança a qualquer momento; as novas regras são aplicadas automaticamente a todas as instâncias associadas ao grupo de segurança.

- Em Regras de grupos de segurança de entrada, selecione Remover

- Neste laboratório, você não fará login na sua instância usando SSH. Remover o acesso SSH melhorará a segurança da instância.

## Etapa 6: Adicionar armazenamento
O Amazon EC2 armazena dados em um disco virtual conectado à rede chamado Amazon Elastic Block Store (Amazon EBS).

- Você inicia a instância EC2 usando um volume de disco padrão de 8 GiB. Este é seu volume raiz (também conhecido como volume de inicialização).

- No painel Configurar armazenamento , mantenha a configuração de armazenamento padrão.

## Etapa 7: Configurando detalhes avançados
Expanda o painel Detalhes avançados .

- Selecione o menu suspenso para Proteção de término e escolha Habilitar .

- Ao iniciar uma instância no Amazon EC2, você tem a opção de passar dados do usuário para a instância. Esses comandos podem ser usados ​​para executar tarefas comuns de configuração automatizada e até mesmo executar scripts após a instância iniciar.

- Copie os seguintes comandos e cole-os na caixa de texto Dados do usuário .

![código usuário](https://github.com/user-attachments/assets/dddaa415-1981-4d51-8bfd-f4a5ca7e695a)

O script faz o seguinte:

- Instalar um servidor web Apache (httpd)

- Configure o servidor web para iniciar automaticamente na inicialização

- Ative o servidor Web

- Crie uma página web simples

## Etapa 8: Iniciando uma instância EC2
Agora que você configurou as configurações da sua instância do EC2, é hora de iniciá-la.

- No painel direito, escolha Iniciar instância

- Selecione Exibir todas as instâncias

A instância aparece em um estado Pendente , o que significa que está sendo iniciada. Em seguida, muda para Running , o que indica que a instância começou a ser inicializada. Haverá um curto período de tempo antes que você possa acessar a instância.

- A instância recebe um nome DNS público que você pode usar para contatá-la pela Internet.

- Selecione o caixa ao lado do seu Web Server . A aba Details exibe informações detalhadas sobre sua instância.

Para ver mais informações na guia Detalhes , arraste o divisor da janela para cima.

Revise as informações exibidas nas guias Detalhes, Segurança e Rede .

- Aguarde até que sua instância exiba o seguinte:

Observação: atualize se necessário.

- Estado da instância: Correndo

- Verificações de status: 2/2 verificações aprovadas

## Tarefa 2: Monitore sua instância
O monitoramento é uma parte importante para manter a confiabilidade, a disponibilidade e o desempenho de suas instâncias do Amazon Elastic Compute Cloud (Amazon EC2) e de suas soluções da AWS.

- Selecione a instância marcando a caixa ao lado dela e navegue até a parte inferior da tela até a guia Verificações de status .

- Com o monitoramento de status de instância, você pode determinar rapidamente se o Amazon EC2 detectou algum problema que possa impedir que suas instâncias executem aplicativos. O Amazon EC2 realiza verificações automatizadas em cada instância EC2 em execução para identificar problemas de hardware e software.

Observe que as verificações de acessibilidade do sistema e da instância foram aprovadas.

- Selecione a aba Monitoramento .

Esta aba exibe métricas do Amazon CloudWatch para sua instância. Atualmente, não há muitas métricas para exibir porque a instância foi lançada recentemente.

Você pode escolher um gráfico para ver uma visualização expandida.

O Amazon EC2 envia métricas para o Amazon CloudWatch para suas instâncias do EC2. O monitoramento básico (cinco minutos) é habilitado por padrão. Você pode habilitar o monitoramento detalhado (um minuto).

- Nas Ações menu, selecione Monitorar e solucionar problemas  Obter captura de tela da instância .

Isso mostra como ficaria o console da sua instância do Amazon EC2 se uma tela fosse anexada a ele.

![instance_screenshot](https://github.com/user-attachments/assets/f2edfc3f-9bf4-4077-85c2-60311017b5cb)

Se você não conseguir acessar sua instância via SSH ou RDP, você pode capturar uma captura de tela da sua instância e visualizá-la como uma imagem. Isso fornece visibilidade quanto ao status da instância e permite uma solução de problemas mais rápida.

- Selecione Cancelar localizado na parte inferior da captura de tela da instância.
Parabéns! Você explorou várias maneiras de monitorar sua instância.

## Tarefa 3: Atualize seu grupo de segurança e acesse o servidor da Web
Ao iniciar a instância EC2, você forneceu um script que instalou um servidor web e criou uma página web simples. Nesta tarefa, você acessará o conteúdo do servidor web.

- Selecione a instância marcando a caixa e selecione a guia Detalhes .

- Copie o endereço IPv4 público da sua instância para a área de transferência.

- Abra uma nova aba no seu navegador, cole o endereço IP que você acabou de copiar e pressione Enter .

Pergunta: Você consegue acessar seu servidor web? Por que não?

No momento, você não consegue acessar seu servidor web porque o grupo de segurança não está permitindo tráfego de entrada na porta 80, que é usada para solicitações da web HTTP. Esta é uma demonstração do uso de um grupo de segurança como um firewall para restringir o tráfego de rede que é permitido dentro e fora de uma instância.

Para corrigir isso, você atualizará o grupo de segurança para permitir tráfego da web na porta 80.

- Mantenha a aba do navegador aberta, mas retorne à aba do Console de Gerenciamento do EC2.

- No painel de navegação esquerdo, selecione Grupos de segurança localizado em Rede e segurança.

- Selecione Grupo de segurança do servidor Web.

- Selecione a aba Regras de entrada.

- O grupo de segurança atualmente não tem regras.

Selecione Editar regras de entrada , depois Adicionar regra e configure a regra com as seguintes configurações:

- Tipo: HTTP 

- Fonte: Anywhere-IPv4 

- Selecione Salvar regras

Retorne à aba do servidor web que você abriu anteriormente e atualizea página.

Você deverá ver a mensagem Olá do seu servidor web!
Parabéns! Você modificou com sucesso seu security group 

## Tarefa 4: Redimensione sua instância: Tipo de instância e volume EBS
Conforme suas necessidades mudam, você pode descobrir que sua instância está sendo superutilizada (muito pequena) ou subutilizada (muito grande). Se for o caso, você pode alterar o tipo de instância . Por exemplo, se uma instância t3.micro for muito pequena para sua carga de trabalho, você pode alterá-la para uma instância m5.medium. Da mesma forma, você pode alterar o tamanho de um disco.

Pare sua instância
Antes de redimensionar uma instância, você deve interrompê -la.

Quando você para uma instância, ela é desligada. Não há cobrança por uma instância EC2 parada, mas a cobrança de armazenamento para volumes Amazon EBS anexados permanece.

- No Console de Gerenciamento do EC2 , no painel de navegação esquerdo, selecione Instâncias .

 - O servidor Web já deve estar selecionado.

- Selecione Estado da instância > Parar instância .

- Selecione Parar
Sua instância executará um desligamento normal e depois deixará de ser executada.

- Aguarde até que o estado da instância seja exibido: parado

Alterar o tipo de instância
- Nas Ações menu, selecione Configurações de instância  Altere o tipo de instância e configure:

- Tipo de instância: t3.small 

- Selecione Aplicar

Quando a instância for iniciada novamente, ela será uma t3.small , que tem o dobro de memória que uma instância t3.micro . NOTA : Você pode estar restrito de usar outros tipos de instância neste laboratório.

## Redimensione o volume do EBS
No menu de navegação à esquerda, selecione Volumes localizado em Elastic Block Store 

- Selecione o volume marcando a caixa e navegue até Açõesmenu, selecione Modificar volume.
O volume do disco atualmente tem um tamanho de 8 GiB. Agora você aumentará o tamanho deste disco.

- Altere o tamanho para: OBSERVAÇÃO : você pode estar restrito a criar grandes volumes do Amazon EBS neste laboratório.10 

- Selecione Modificar

- Selecione Modificar para confirmar e aumentar o tamanho do volume.

## Inicie a instância redimensionada
Agora você iniciará a instância novamente, que agora terá mais memória e mais espaço em disco.

- No painel de navegação esquerdo, selecione Instâncias.

- Selecione a instância do Servidor Web marcando a caixa e navegue até Estado da instância > Iniciar instância.

Parabéns! Você redimensionou com sucesso sua instância do Amazon EC2. Nesta tarefa, você alterou seu tipo de instância de t3.micro para t3.small . Você também modificou seu volume de disco raiz de 8 GiB para 10 GiB.

## Tarefa 5: Proteção de Término de Teste
Você pode excluir sua instância quando não precisar mais dela. Isso é conhecido como encerramento de sua instância. Você não pode se conectar ou reiniciar uma instância após ela ter sido encerrada.
Nesta tarefa, você aprenderá como usar a proteção de terminação.

- No painel de navegação esquerdo, selecione Instâncias.

- Selecione a instância do servidor Web marcando a caixa e navegue até o topo e selecione Estado da instânciamenu, selecione Encerrar instância.

Observação: há uma mensagem que diz: Em uma instância com suporte do EBS, a ação padrão é que o volume raiz do EBS seja excluído quando a instância for encerrada. O armazenamento em qualquer unidade local será perdido. Ele perguntará se você tem certeza de que deseja encerrar a instância. Você poderá selecionar o botão Terminate 

Nota: Você notará que a instância não foi encerrada e uma mensagem de erro vermelha aparece no topo dizendo: Falha ao encerrar uma instância: A instância pode não ser encerrada. Isso ocorre porque ela tem a proteção de encerramento habilitada.

- Nas Ações menu, selecione Configurações de instância  Alterar proteção de término .

- Desmarcar Habilitar seguido de Salvar

Agora você pode encerrar a instância.

- Nas Ações menu, selecione Estado da Instância  Encerrar instância .

- Selecione Terminar

Parabéns! Você testou com sucesso a proteção de encerramento e encerrou sua instância.




