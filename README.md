# CondoCheck

Gestão e manutenção do **Condomínio Portale Mattino**: chamados, controle de piscinas e prazos obrigatórios, em português.

Arquivo único (`app.html`, com HTML, CSS e JavaScript). Roda como **artefato Claude**: usa o banco de dados, o login, o upload de fotos, os downloads e a IA do próprio Claude. Aberto como arquivo solto no navegador, mostra "Banco de dados indisponível".

## O que tem
- **Perfis:** Administração, Manutenção e Portaria.
- **Início:** painel com chamados abertos, em atendimento, pausados e urgentes (cada número abre a lista filtrada), última leitura da piscina e situação dos prazos obrigatórios.
- **Chamados:** abrir, assumir, pausar, concluir, com histórico. Ao assumir, a Manutenção faz a verificação de EPI (a lista é ajustada em Configurações).
- **Preventivas:** rotinas programadas que geram chamado. A Administração cadastra; a Manutenção vê e gera o chamado.
- **Rondas:** a Administração cria os roteiros; a Portaria faz o checklist e cada ponto com problema abre um chamado na hora.
- **Checklist de espaços:** a Portaria faz o check-in de qualquer espaço, com ou sem reserva. Depois de iniciado, o checklist fica **Em andamento** e só se encerra com o **checkout** no fim do evento (o checkout mostra a entrada para comparar; ressalva exige foto e abre um possível chamado, marcado como NOVO se a entrada estava em ordem). Um espaço não aceita dois check-ins abertos; a Administração pode cancelar um aberto por engano. Cada checklist exporta **PDF** (com ou sem fotos) e envia por **WhatsApp**, **e-mail** ou **Compartilhar**. No artefato o app não anexa arquivos sozinho: o PDF é baixado e o WhatsApp/e-mail abre com a mensagem pronta para anexar (no celular, Compartilhar já anexa).
- **Reservas / Vistorias:** a Administração registra e aprova a reserva de um espaço; a Portaria faz a vistoria de entrada e de saída com o checklist daquele espaço, com assinaturas. Ressalvas viram possíveis chamados. O termo de vistoria sai em PDF, por e-mail ou WhatsApp.
- **Piscinas:** registro de pH, cloro, alcalinidade, reagentes e visto do gerente. Leitura fora do ideal abre chamado sozinha.
- **Equipe e custo-hora:** a Administração cadastra os funcionários em Pessoas / Funcionários (＋ Cadastrar pessoa → Funcionário → perfil Manutenção) e, na mesma tela, informa o salário, os encargos e as horas por mês de cada um; o sistema calcula o valor da hora e usa no custo de mão de obra dos chamados e no desempenho da equipe. Os valores ficam numa coleção própria (`rh`), carregada só para a Administração.
- **Controle de EPI:** ficha de entrega por funcionário (item, nº do CA, tamanho, quantidade, data, validade, devolução), com aviso na tela inicial 30 dias antes de vencer. A Administração registra; a Manutenção vê só o seu. A verificação de EPI ao assumir um chamado continua.
- **Quem vê o quê:** em Configurações → “Quem vê o quê”, a Administração desmarca os módulos que a Manutenção ou a Portaria não devem ver (por exemplo, Orçamentos). Some do menu, da tela inicial e dos avisos.
- **Compras:** Orçamentos e Cotações (Administração e Manutenção), além de Estoque com lista de compras, importar lista (Excel/CSV, só a Administração) e exportar. Também: Biblioteca de documentos, Centro de Custos, Calendário, Automações e Auditoria.
- **Cadastro mestre:** equipamentos, etiquetas QR, espaços e estoque.
- **Contratos, Garantias e Fornecedores.**
- **Obrigações e Conformidade:** AVCB, extintores, elevadores, reservatórios, dedetização, seguro predial e outros, com alertas de 90, 60 e 30 dias. A Administração cadastra; a Manutenção consulta. **A Portaria não vê Obrigações nem Piscinas** (nem alertas, cartões ou calendário delas).
- **Só para a Administração:** Saúde da Manutenção, Tendências Executivas, Reincidências, Desempenho da equipe, Central de Relatórios, Pessoas / Funcionários e Configurações.
- **Quem vê e edita** segue as regras do código. A tabela de permissões salva no banco pelo PredialFlow é ignorada.
- **Portale Mattino já carregado:** 8 torres (Gênova, Trivento, Turim, Roma, Tivoli, Modena, Positano, Savona) e piscinas Adulto (143 mil litros) e Infantil (17 mil litros) vêm dentro do código.

## Dados do banco
O app lê espaços e checklists do banco. Um banco novo começa vazio, então as telas de Espaços e de vistoria aparecem sem nada. Os dados do Portale Mattino estão em `dados/portale-mattino.json`: 5 espaços (Lounge Gourmet, Salão de Festas Adulto, Salão de Festas Infantil, Churrasqueira Gourmet, Churrasqueira Quadra) e o checklist de vistoria de cada um. Os espaços vão na coleção `espacos`, um documento por id, e o checklist no documento `ajustes/checklist`. Horários, capacidade e regras de reserva de cada espaço ainda não estão cadastrados.

## Origem
Derivado do PredialCheck (`dgstuning/predialcheck`, branch `simplificado-portale-mattino`), reduzido aos módulos acima. Os demais módulos do PredialFlow continuam escondidos no código e serão podados aos poucos.

## Próximo passo
Trocar a camada de dados do Claude por um servidor próprio. Os pontos de contato são cinco: banco (`db`), usuário (`user`), fotos (`assets`), downloads (`downloads`) e IA (`sample`).
