Trabalho de Graduação 1

1- Problema
Dificuldade de gestão do serviço de outsourcing de impressão.

2- Motivação (Porque o problema é um problema)
Devido ao alto volume de impressão, falta de mão de obra qualificada para manutenção, diversidade de modelos e marcas de equipamentos, o custo elevado de consumíveis e das peças, a opção de adotar um sistema de outsourcing de impressão começou a ser estudado e posteriormente adotado pela Empresa.
O primeiro contrato baseava-se em uma franquia com um volume de impressão mínimo mensal pré-estabelecido. Se o número de impressões superasse essa franquia, o excedente era cobrado por página impressa, além disso, impressoras adicionais tinham um custo adicional, variando de preço dependendo do modelo e do tipo de equipamento. As manutenções preventivas e corretivas também estavam englobadas no contrato. 
Dado o início do contrato, foi feito uma vistoria nos equipamentos da empresa e os equipamentos que precisaram de manutenção corretiva ou preventiva foram levados para a empresa para o procedimento.
Logo no início do contrato surgiu o primeiro problema, a coleta dos contadores de impressão era feita de modo manual, onde o técnico se deslocava até o local de instalação de cada equipamento e imprimia o relatório da impressora. Este método era inviável pois ao imprimir estes relatórios, desperdiçava-se muitas folhas e a empresa pagava por estas páginas impressas, além de ocupar o tempo de um colaborador para realizar tal tarefa. 
Outros problemas foram surgindo no decorrer do contrato, suprimentos com vazamento de toner e de má qualidade e chamados de manutenção sem atendimento e mão de obra desqualificada. Isso tudo além de prejudicar o andamento dos trabalhos cotidianos da empresa, deixava a equipe de Service Desk com inúmeros chamados, atrasando o atendimento de outras demandas.
Devido a estes problemas sem soluções e o fato de que ao renovar o contrato haveria um reajuste, surgiu a necessidade de buscar outras soluções no mercado, foi dado então o início de um projeto de troca de fornecedores.
Este projeto consistia em alocar equipamentos de um mesmo fabricante e modelo para centralizar e facilitar o gerenciamento dos suprimentos, máquinas com maiores capacidades de impressão por minuto, suprimentos originais ou paralelos e a coleta dos dados deveria ser de maneira automática. Quanto à manutenção, o requisito era de um tempo de atendimento de no máximo 36 horas.
Foi elaborado um documento de requisitos e enviado às empresas. Após receber todas as propostas, foi feito uma análise e as empresas que não atenderam os requisitos já foram eliminadas nesta fase. O critério de escolha foi o menor preço.
Definido a empresa que seria contratada, foi elaborado um plano de implementação pois no contrato vigente no momento havia uma cláusula de exclusividade, impossibilitando a troca previa dos equipamentos. No dia do encerramento, foi mobilizado equipes da empresa vencedora e do Service Desk da empresa para distribuir os equipamentos priorizando os setores críticos. A implantação foi realizada com alguns problemas, porém contornados rapidamente.
Após a implementação, a solução oferecida de coleta de dados dos equipamentos foi o software Print Supervision da empresa Oki Data, parceira da empresa contratada. Após configurar todos os equipamentos no software, foi configurado o envio de e-mails com os relatórios.
Esta aplicação atende os requisitos solicitados, porém surgiu a necessidade de auditar os dados recebidos da empresa e de manter um histórico de produção de cada equipamento.
 
3- Proposta de solução

A solução proposta para este problema, é implementar uma aplicação que colete as informações dos equipamentos através do protocolo SNMP (Simple Network Management Protocol) e armazene-as em um banco de dados para ter os dados de hora em hora de cada equipamento. Mensalmente a empresa recebe uma fatura com o detalhamento de produção de cada equipamento, ao salvar o faturamento na pasta do histórico acionará uma trigger que imporá os dados do faturamento e comparará com os dados coletados pelo agente coletor. Após comparar os dados e se os dados forem coerentes, acionará uma outra trigger e enviará a produção de cada equipamento ao gestor responsável por cada impressora.
 
Requisitos funcionais:

•	O servidor deverá ter a máquina virtual Java instalada.
•	O servidor deverá estar conectado em rede.
•	Os equipamentos deverão preferencialmente estar conectados em rede.
•	Os equipamentos deverão se comunicar com o servidor via protocolo SNMP.
•	O sistema coletará os dados das impressoras de rede de hora em hora.
•	O sistema solicitará ao administrador semanalmente que insira manualmente o contador dos equipamentos que não estejam ligados em rede.
•	O sistema deverá receber o faturamento detalhado de cada mês e inserir no histórico.
•	O sistema comparará os dados do coletor com os dados recebidos através do faturamento.
•	O sistema enviará mensalmente e-mails para os gestores com as estatísticas mensais, porém restringindo as informações dos equipamentos a seu respectivo gestor.
•	O administrador fará o cadastramento de impressoras, setores, gestores e usuários.

Requisitos não funcionais:

•	Usabilidade, o sistema terá uma interface web amigável e intuitiva.
•	Manutenibilidade, o sistema deverá ser construído de maneira organizada de modo que outros desenvolvedores possam facilmente entender o sistema e dar suporte ou até mesmo agregar novas funções.
•	Portabilidade, o sistema deverá contemplar a possibilidade de portabilidade para plataformas Android, de modo que facilite o administrador em suas tarefas.
•	Segurança, o sistema deverá separar os interesses de cada gestor e realizar o controle de acesso dos administradores.
•	O sistema será executado em um servidor em rede.
•	Os dados devem ser armazenados em um banco de dados relacional.

Diagrama Entidade - Relacionamento: 

 







Diagrama de Caso de uso: 

Sistema: 

 :

Administrador: 

 
 
Técnicas e ferramentas necessárias:

O sistema será desenvolvido em linguagem de programação Java utilizando a arquitetura Model-View-Controller (MVC), através do ambiente de desenvolvimento Eclipse IDE. Para fazer a comunicação da aplicação com a impressora, a biblioteca SNMP4J será utilizada. 

Arquitetura MVC (Model – View - Controller) (MVC, Afinal, é o quê ?)

O MVC é um padrão de arquitetura de software, que separa a aplicação em 3 camadas. A camada de interação do usuário (view), a camada de manipulação dos dados (model) e a camada de controle (controller).

Model
É responsável pela leitura e escrita de dados, e também de suas validações.

View
É a camada de interação com o usuário. Faz apenas a exibição dos dados.

Controller
É o responsável por receber todas as requisições do usuário. Seus métodos chamados são responsáveis por uma página, controlando qual model usar e qual view será mostrado ao usuário.

(A imagem abaixo representa o fluxo do MVC em um contexto de Internet, com uma requisição HTTP e resposta em formato HTML ou XML)
 
 

Protocolo SNMP (https://www.4linux.com.br/o-que-e-snmp)

O SNMP é um protocolo usado para saber o que acontece dentro de ativos de redes e serviços. Praticamente qualquer ativo de rede gerenciável se comunica através deste protocolo e diversos serviços usam SNMP como protocolo de gerenciamento. 
O SNMP foi criado para facilitar o monitoramento e gerenciamento de redes permitindo que uma ferramenta de gerenciamento possa trabalhar com produtos e serviços de diversos fabricantes.
Neste protocolo, o item a ser monitorado ou gerenciado é um agente. Quem consulta (GET) ou solicita modificações (SET) é um gerente. O agente também tem a função de gerar alertas (TRAP).
O sistema gerente pode usar estes alertas para gerar alarmes visuais ou usar ferramentas de comunicação como SMS e e-mail para avisar os responsáveis.
O agente SNMP, contempla uma tabela de informações que pode ser consultada ou modificada pelo sistema gerente.
Para que esta consulta possa ser feita, o gerente tem que conhecer as informações que podem ser obtidas do agente SNMP. Isso é garantido pelo uso de algo semelhante a um dicionário de dados: MIB e OID. 
A MIB é base de informações de gerenciamento e um OID é o identificador único dentro da MIB.
O OID de um dispositivo ou serviço está dentro de uma hierarquia inscrita em https://www.iana.org/. Esta hierarquia reserva "pedaços" da árvore para fabricantes e instituições que podem usar os identificadores para uso em SNMP.
Repositório MIB e OID: http://oid-info.com/index.htm

Para este projeto, usarei os OIDs abaixo:

ASN.1 {iso(1) identified-organization(3) dod(6) internet(1) mgmt(2) mib-2(1) system(1)}
OID_sysContact (1.3.6.1.2.1.1.4.0)
OID_sysLocation (1.3.6.1.2.1.1.6.0)

ASN.1 {iso(1) identified-organization(3) dod(6) internet(1) mgmt(2) mib-2(1) host(25)}
OID_hrDeviceDescr (1.3.6.1.2.1.25.3.2.1.3.1)
OID_hrDeviceStatus (1.3.6.1.2.1.25.3.2.1.5.1)
OID_hrPrinterStatus (1.3.6.1.2.1.25.3.5.1.1.1)

ASN.1 {iso(1) identified-organization(3) dod(6) internet(1) mgmt(2) mib-2(1) printmib(43)}
OID_prtSerialNumber (1.3.6.1.2.1.43.5.1.1.17.1)
OID_prtMarkerSuppliesMaxCapacity (1.3.6.1.2.1.43.11.1.1.8.1.1)
OID_prtMarkerSuppliesLevel (1.3.6.1.2.1.43.11.1.1.9.1.1)
OID_prtMarkerSuppliesType (1.3.6.1.2.1.43.11.1.1.5.1.1)
OID_prtMarkerSuppliesDescription (1.3.6.1.2.1.43.11.1.1.6.1.1)
OID_prtMarkerLifeCount (1.3.6.1.2.1.43.10.2.1.4.1.1)

 

SNMP4J – O SNMP Orientado a objeto. (https://www.snmp4j.org/)

SNMP4J é um open source gratuito de classe empresarial de última geração para implementação de gerencai de agentes via SNMP para Java SE 8 ou posterior. O SNMP4J suporta a geração de comandos (gerenciadores), bem como comandos de resposta (agentes). Seu design limpo e orientado a objetos é inspirado pelo SNMP ++, que é uma API conhecida SNMPv1 / v2c / v3 para C ++.
