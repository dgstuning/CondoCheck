# CondoCheck

Gestão e manutenção do **Condomínio Portale Mattino**: chamados, controle de piscinas e prazos obrigatórios, em português.

Arquivo único (`app.html`, com HTML, CSS e JavaScript). Roda como **artefato Claude**: usa o banco de dados, o login, o upload de fotos, os downloads e a IA do próprio Claude. Aberto como arquivo solto no navegador, mostra "Banco de dados indisponível".

## O que tem
- **Perfis:** Administração, Manutenção e Portaria.
- **Início:** painel com chamados abertos, em atendimento, pausados e urgentes (cada número abre a lista filtrada), última leitura da piscina e situação dos prazos obrigatórios.
- **Chamados:** abrir, assumir, pausar, concluir, com histórico. Ao assumir, a Manutenção faz a verificação de EPI (a lista é ajustada em Configurações).
- **Preventivas:** rotinas programadas que geram chamado. A Administração cadastra; a Manutenção vê e gera o chamado.
- **Rondas:** a Administração cria os roteiros; a Portaria faz o checklist e cada ponto com problema abre um chamado na hora.
- **Piscinas:** registro de pH, cloro, alcalinidade, reagentes e visto do gerente. Leitura fora do ideal abre chamado sozinha.
- **Cadastro mestre:** equipamentos, etiquetas QR, espaços e estoque.
- **Contratos, Garantias e Fornecedores.**
- **Obrigações e Conformidade:** AVCB, extintores, elevadores, reservatórios, dedetização, seguro predial e outros, com alertas de 90, 60 e 30 dias. A Administração cadastra; Manutenção e Portaria consultam.
- **Só para a Administração:** Saúde da Manutenção, Tendências Executivas, Reincidências, Desempenho da equipe, Central de Relatórios, Pessoas / Funcionários e Configurações.
- **Quem vê e edita** segue as regras do código. A tabela de permissões salva no banco pelo PredialFlow é ignorada.
- **Portale Mattino já carregado:** 8 torres (Gênova, Trivento, Turim, Roma, Tivoli, Modena, Positano, Savona) e piscinas Adulto (143 mil litros) e Infantil (17 mil litros).

## Origem
Derivado do PredialCheck (`dgstuning/predialcheck`, branch `simplificado-portale-mattino`), reduzido aos módulos acima. Os demais módulos do PredialFlow continuam escondidos no código e serão podados aos poucos.

## Próximo passo
Trocar a camada de dados do Claude por um servidor próprio. Os pontos de contato são cinco: banco (`db`), usuário (`user`), fotos (`assets`), downloads (`downloads`) e IA (`sample`).
