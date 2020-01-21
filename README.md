# README
Usei como meu sistema operacional o Ubuntu Server 18.04.
Escolhi utilizar Ansible para essa tarefa pois já conhecia o básico da ferramenta.
Inicialmente adicionei ao arquivo "hosts" o endereço ip do servidor (com ssh liberado). 
Optei por não criptografar ("ansible-vault encrypt "), para não ser necessário passar senha. Obs: removi as informações sensíveis do servidor do arquivo "hosts"
Realizei os testes na minha máquina AWS
Na playbook do ansible não especifiquei o tipo de sistema operacional, pois como todos estavam utilizando ubuntu o módulo 'apt' funciona normalmente.
Percebi que, ainda de acordo com os fóruns, o Ansible não possui um comando direto para o 'pipenv', para contornar a situação, utilizei o módulo 'shell'.
Como seria necessário ter dois processos simultâneos em execução, o "minio" e a aplicação, não consegui fazer com que executassem na mesma playbook ou que algum dos dois processos seja executado no backend, ainda estou pesquisando sobre isso. Por essa razão, dividi a playbook em duas partes:
--Na primeira parte "firststeps.yml" as bibliotecas necessárias são instaladas, optei por instalar o 'gunicorn' de forma externa para que pudesse ser reaproveitados em outras pipenv. Também optei por instalar 'pipenv', o 'minio', configurar e executar o minio. 
-- A segunda parte "secondstep.yml" é responsável por instalar as dependências do "Pipfile", clonar o código no github, iniciar o 'pipenv' e executar a aplicação.

Como possuo conhecimento básico da plataforma, não consegui fazer com que as playbooks fossem executadas de forma simultânea, sendo necessário executar a primeira playbook e, por fim, executar a segunda, mantendo ambas em execução.
Para executar são necessários dois terminais,
No primeiro terminal, basta executar (com ansible instalado): 'ansible-playbook -i hosts firststep.yml'.
Ao executar a task 'execute minio', no segundo terminal, executa 'ansible-playbook -i hosts secondstep.yml'.
Ao executar a task 'start shell n execute app' a aplicação poderá ser usada.

Obrigado!

