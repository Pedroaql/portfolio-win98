# Portfolio Win98 - HomeLab

Este projeto é um portfólio pessoal com estética "Windows 98", conteinerizado via Docker e automatizado com GitHub Actions para deploy contínuo em servidor próprio.

## Arquitetura
* **Frontend:** HTML5, CSS customizado (estética Win98), Vanilla JS.
* **Servidor Web:** Nginx (via imagem `nginx:alpine`).
* **Orquestração:** Docker Compose.
* **CI/CD:** GitHub Actions (automação via `git pull` e `docker-compose up`).

## Estrutura de Pastas
```text
/
├── .github/workflows/main.yml  # Automação de deploy
├── docker-compose.yml          # Configuração do container
└── web/                        # Arquivos do site (HTML/CSS/JS)
    └── index.html

Como configurar o Servidor (Deploy)
1. Pré-requisitos
Docker e Docker Compose instalados no servidor.
Acesso via SSH.
2. Execução manual
Para subir o serviço manualmente no servidor:
# Na raiz do repositório
docker-compose up -d --force-recreate

3. Sincronização (GitHub Actions)
O pipeline está configurado para, a cada git push na branch main:
Acessar o diretório do projeto no servidor.
Executar git pull origin main.
Reiniciar o container com as novas alterações

Resolução de Problemas
Site "pelado" (sem estilo): O navegador não está encontrando os arquivos .css.
Solução: Verifique se todos os arquivos CSS estão dentro da pasta /web e se os links no index.html são caminhos relativos (ex: href="7.css").
Erro "Address already in use": A porta 80 do servidor está ocupada.
Solução: Edite o docker-compose.yml, altere a porta mapeada (ex: 8080:80) e acesse via IP:8080.
Erro de Push (Rejected): Existe divergência entre o seu PC e o GitHub.
Solução: Execute git pull origin main no seu computador antes de fazer um novo push.
