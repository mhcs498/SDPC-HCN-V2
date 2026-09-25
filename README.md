# SDPC-HCN-V2
Sistema Digital do Processo de Internamento — Hospital Central de Nampula
# SDPC-HCN â€” Sistema Digital do Processo ClÃ­nico
### Hospital Central de Nampula Â· RepÃºblica de MoÃ§ambique Â· MinistÃ©rio da SaÃºde (SNS)

O **SDPC-HCN** Ã© uma plataforma hospitalar e prontuÃ¡rio mÃ©dico eletrÃ³nico concebida para digitalizar a gestÃ£o clÃ­nica, internamento, acompanhamento intensivo e estatÃ­sticas do Hospital Central de Nampula (HCN), a maior unidade sanitÃ¡ria de referÃªncia da regiÃ£o norte de MoÃ§ambique.

---

## ðŸ“Œ SumÃ¡rio
1. [VisÃ£o Geral & MÃ³dulos](#-visÃ£o-geral--mÃ³dulos)
2. [Estrutura do Sistema & FormulÃ¡rios ClÃ­nicos](#-estrutura-do-sistema--formulÃ¡rios-clÃ­nicos)
3. [Tecnologias Utilizadas](#-tecnologias-utilizadas)
4. [ConfiguraÃ§Ã£o do Ambiente Local (Passo a Passo)](#-configuraÃ§Ã£o-do-ambiente-local-passo-a-passo)
   - [OpÃ§Ã£o 1: ExecuÃ§Ã£o Direta (Sem Node.js)](#opÃ§Ã£o-1-execuÃ§Ã£o-direta-sem-nodejs)
   - [OpÃ§Ã£o 2: Servidor de Desenvolvimento Vite + Node.js](#opÃ§Ã£o-2-servidor-de-desenvolvimento-vite--nodejs)
   - [OpÃ§Ã£o 3: Servidor Local com Python ou PHP](#opÃ§Ã£o-3-servidor-local-com-python-ou-php)
   - [OpÃ§Ã£o 4: Docker & Nginx](#opÃ§Ã£o-4-docker--nginx)
5. [Credenciais PadrÃ£o & SeguranÃ§a](#-credenciais-padrÃ£o--seguranÃ§a)
6. [Armazenamento & PersistÃªncia de Dados](#-armazenamento--persistÃªncia-de-dados)
7. [RelatÃ³rios EstatÃ­sticos & Indicadores de GestÃ£o (TOC)](#-relatÃ³rios-estatÃ­sticos--indicadores-de-gestÃ£o-toc)
8. [Estrutura de Ficheiros do Projeto](#-estrutura-de-ficheiros-do-projeto)
9. [SoluÃ§Ã£o de Problemas (Troubleshooting)](#-soluÃ§Ã£o-de-problemas-troubleshooting)

---

## ðŸ¥ VisÃ£o Geral & MÃ³dulos

O sistema divide-se em dois fluxos principais com acesso segmentado:

### 1. Portal PÃºblico (CidadÃ£os)
- **MarcaÃ§Ã£o Online de Consultas**: FormulÃ¡rio com validaÃ§Ã£o de Nome, Contacto TelefÃ³nico, Bilhete de Identidade (BI), SeleÃ§Ã£o de ProveniÃªncia (Distritos da ProvÃ­ncia de Nampula: Cidade, Nacala, Ilha de MoÃ§ambique, RibÃ¡uÃ¨, Moma, etc.) e Motivo da Consulta.
- **Protocolo Ãšnico**: GeraÃ§Ã£o automÃ¡tica de comprovativo (`APT-XXXXXX`) armazenado em fila de agendamento.

### 2. Portal dos Profissionais de SaÃºde
Acesso direcionado para os 10 departamentos clÃ­nicos do HCN:
1. `BS` â€” Banco de Socorros
2. `CE` â€” Consulta Externa
3. `Ped` â€” Pediatria
4. `G.Obs` â€” Ginecologia e ObstetrÃ­cia
5. `Cir` â€” Cirurgia Geral
6. `Orto` â€” Ortopedia e Traumatologia
7. `Neuroc` â€” Neurocirurgia
8. `Med.I` â€” Medicina Interna
9. `SRA` â€” ServiÃ§o de ReanimaÃ§Ã£o Adulto (Cuidados Intensivos/UrgÃªncia)
10. `Onco` â€” Oncologia

---

## ðŸ“‹ Estrutura do Sistema & FormulÃ¡rios ClÃ­nicos

O SDPC-HCN padroniza a documentaÃ§Ã£o hospitalar atravÃ©s de 8 formulÃ¡rios e um Painel Geral (Dashboard):

- **ðŸ  Painel Principal (Dashboard)**: Resumo em tempo real com estatÃ­sticas (Doentes registados, atualizados no dia, formulÃ¡rios preenchidos, taxa de preenchimento global), atalhos de aÃ§Ãµes rÃ¡pidas, e lista dos doentes mais recentes.
- **F1 â€” Internamento Geral**: Dados demogrÃ¡ficos, registo de admissÃ£o, acompanhantes de referÃªncia e emergÃªncia, atribuiÃ§Ã£o de cama/serviÃ§o, tipo de admissÃ£o (1 a 9) e motivo de admissÃ£o (1 a 6).
- **F2 â€” HistÃ³ria ClÃ­nica (Anamnese)**: Queixas principais, histÃ³ria da doenÃ§a atual, antecedentes mÃ©dicos e patologias pregressas (HTA, DM, Asma, TB, etc.), histÃ³ria familiar, histÃ³rico psicossocial e RevisÃ£o por Sistemas (ROS em 16 sistemas).
- **F3 â€” Exame FÃ­sico**: Estado geral, Escala de Coma de Glasgow, constantes vitais (TA, FC, FR, Temp, SpOâ‚‚, Glicemia, IMC), cabeÃ§a e pescoÃ§o, auscultaÃ§Ã£o cardiopulmonar, palpaÃ§Ã£o abdominal, exames especiais e hipÃ³teses de diagnÃ³stico.
- **F4 â€” Registo ClÃ­nico de SaÃ­da**: Tipo de alta (Curado, Melhorado, TransferÃªncia, etc.), complicaÃ§Ãµes, cÃ¡lculo automÃ¡tico dos dias de hospitalizaÃ§Ã£o, ClassificaÃ§Ã£o Internacional/OMS e bloco de Registo de Ã“bito e EspÃ³lio.
- **F5 â€” DiÃ¡rio ClÃ­nico**: EvoluÃ§Ã£o mÃ©dica por turno, prescriÃ§Ã£o e tratamentos, registo de anÃ¡lises laboratoriais e exames imagiolÃ³gicos (Rx, TAC, Ecografia) com upload de imagens mÃ©dicas em Base64 e zoom modal.
- **F6 â€” DiÃ¡rio de Enfermagem**: Registo de evoluÃ§Ã£o pelo corpo de enfermagem, horÃ¡rios de administraÃ§Ã£o medicamentosa, monitorizaÃ§Ã£o de sinais vitais e procedimentos invasivos.
- **F7 â€” DiÃ¡rio ClÃ­nico SRA**: MÃ³dulo especÃ­fico para ReanimaÃ§Ã£o e Cuidados Intensivos com cÃ¡lculo automÃ¡tico da Escala de Glasgow (AO + RV + RM = 3 a 15), dispositivos invasivos (SNG, CVP, Algalea), balanÃ§o de extremos de 24h e prognÃ³stico.
- **F8 â€” MonitorizaÃ§Ã£o SRA & Curvas Vitais**:
  - **Curvas GrÃ¡ficas Interativas (24h)**: Pontos clicÃ¡veis com desenho SVG contÃ­nuo para TensÃ£o Arterial SistÃ³lica (60-220 mmHg), Pulso (40-180 bpm) e Temperatura (34-42 Â°C).
  - **Grelha de Fluidoterapia (24h)**: Controlo rigoroso de Entradas (soros/medicaÃ§Ã£o) vs. SaÃ­das (urina e perdas/drenos) com cÃ¡lculo dinÃ¢mico do BalanÃ§o HÃ­drico horariamente.

---

## ðŸ’» Tecnologias Utilizadas

- **Frontend & Interface**: HTML5 semÃ¢ntico, CSS3 (CSS Grid, Flexbox, VariÃ¡veis CSS, Glassmorphism e estilos dedicados para impressÃ£o `@media print`).
- **LÃ³gica & Interatividade**: JavaScript Vanilla (ES6+) moderno com tipagem flexÃ­vel e manipulaÃ§Ã£o nativa de DOM.
- **Criptografia**: Web Cryptography API (`crypto.subtle.digest('SHA-256')`) com salt para armazenamento seguro de credenciais.
- **Armazenamento**: LocalStorage API estruturado para funcionamento 100% autÃ´nomo e sem falhas de conexÃ£o de rede.
- **GrÃ¡ficos & Imagiologia**: SVG dinÃ¢mico gerado em tempo real e FileReader API para imagens mÃ©dicas.
- **ExportaÃ§Ã£o & RelatÃ³rios**: GeraÃ§Ã£o em Blob de ficheiros compatÃ­veis com Microsoft Word (`.doc`) e Microsoft Excel (`.xls`), e folha de estilo A4 para impressoras fÃ­sicas.

---

## ðŸ› ï¸ ConfiguraÃ§Ã£o do Ambiente Local (Passo a Passo)

### PrÃ©-requisitos Recomendados
- **Navegador Web**: Qualquer navegador moderno com suporte a ES6 e Web Cryptography (Google Chrome, Mozilla Firefox, Microsoft Edge, Safari ou Brave).
- **Node.js (Opcional, para execuÃ§Ã£o com Vite)**: VersÃ£o 18.x ou 20.x LTS (caso opte pelo ambiente Vite/NPM).

---

### OpÃ§Ã£o 1: ExecuÃ§Ã£o Direta (Sem Node.js â€” Mais RÃ¡pida)

Como o arquivo original Ã© autocontido (Single File Component):

1. **Baixar ou clonar o projeto**:
   ```bash
   git clone <URL_DO_REPOSITORIO>
   cd <PASTA_DO_PROJETO>
   ```
2. **Abrir diretamente o arquivo no navegador**:
   - DÃª um duplo clique no arquivo `sdpc-hcn.html` ou
   - Clique com o botÃ£o direito -> **Abrir com** -> **Google Chrome** (ou seu navegador de preferÃªncia).
3. **Ou atravÃ©s do terminal**:
   - **Linux**: `xdg-open sdpc-hcn.html`
   - **macOS**: `open sdpc-hcn.html`
   - **Windows**: `start sdpc-hcn.html`

> ðŸ’¡ *Dica*: Esta opÃ§Ã£o nÃ£o requer instalaÃ§Ã£o de pacotes ou servidores, ideal para computadores de enfermarias ou locais com internet limitada.

---

### OpÃ§Ã£o 2: Servidor de Desenvolvimento Vite + Node.js (Ambiente Completo)

Se estiver utilizando a estrutura de workspace com React, Vite e Tailwind CSS:

1. **Verificar a versÃ£o do Node.js e NPM**:
   ```bash
   node -v
   npm -v
   ```
   *(Recomenda-se Node.js >= 18.0.0)*

2. **Instalar as dependÃªncias do projeto**:
   ```bash
   npm install
   ```

3. **Configurar as VariÃ¡veis de Ambiente**:
   Copie o arquivo de exemplo para criar o `.env`:
   ```bash
   cp .env.example .env
   ```
   *(Se for utilizar rotas de IA opcionais, configure a sua `GEMINI_API_KEY`, caso contrÃ¡rio deixe com o valor padrÃ£o)*

4. **Iniciar o Servidor Local**:
   ```bash
   npm run dev
   ```
   O terminal exibirÃ¡ o endereÃ§o local:
   ```text
   VITE v6.x / v8.x ready in 250 ms

   âžœ  Local:   http://localhost:3000/
   âžœ  Network: http://<seu-ip>:3000/
   ```

5. **Acessar a aplicaÃ§Ã£o**:
   Abra `http://localhost:3000` no seu navegador. O aplicativo carregarÃ¡ o portal integrado com a documentaÃ§Ã£o interativa e o sistema SDPC-HCN em tempo real.

6. **Para compilar a versÃ£o final para produÃ§Ã£o**:
   ```bash
   npm run build
   ```
   Os arquivos otimizados serÃ£o gerados na pasta `dist/`.

---

### OpÃ§Ã£o 3: Servidor Local Leve (Python ou PHP)

Se vocÃª nÃ£o tiver Node.js instalado mas deseja servir via protocolo HTTP (evitando restriÃ§Ãµes do protocolo `file://`):

- **Com Python 3**:
  ```bash
  python3 -m http.server 8080
  ```
  Acesse no navegador: `http://localhost:8080/sdpc-hcn.html`

- **Com PHP**:
  ```bash
  php -S localhost:8080
  ```
  Acesse no navegador: `http://localhost:8080/sdpc-hcn.html`

- **Com a extensÃ£o "Live Server" do VS Code**:
  1. Abra o arquivo no VS Code.
  2. Clique no botÃ£o **"Go Live"** na barra inferior.

---

### OpÃ§Ã£o 4: Docker & Nginx (Para ImplantaÃ§Ã£o em Rede Local Hospitalar)

Para instalar num servidor local da intranet hospitalar usando Docker:

1. Crie um arquivo `Dockerfile`:
   ```dockerfile
   FROM nginx:alpine
   COPY sdpc-hcn.html /usr/share/nginx/html/index.html
   EXPOSE 80
   CMD ["nginx", "-g", "daemon off;"]
   ```
2. Construa a imagem e inicie o contentor:
   ```bash
   docker build -t sdpc-hcn .
   docker run -d -p 80:80 --name hospital-central sdpc-hcn
   ```
3. O sistema estarÃ¡ acessÃ­vel em qualquer computador da rede local hospitalar pelo IP do servidor: `http://<IP_DO_SERVIDOR>/`.

---

## ðŸ” Credenciais PadrÃ£o & SeguranÃ§a

1. **Primeiro Acesso (Bootstrap Admin)**:
   - Ao iniciar pela primeira vez sem dados cadastrados, selecione qualquer departamento (ex: `Med.I` ou `BS`) e clique em **"Criar conta"**.
   - **O primeiro utilizador registado assume automaticamente o papel de Administrador (`admin`)**.
2. **Novos Utilizadores Criados pelo Admin**:
   - No painel de **GestÃ£o de Utilizadores** (botÃ£o `ðŸ‘¥ Utilizadores` visÃ­vel apenas para administradores), o gestor pode criar novas contas definindo nome, username, departamento e permissÃ£o (`user` ou `admin`).
   - A senha inicial padrÃ£o para contas adicionadas via painel Ã©: **`1234`**.
3. **Criptografia**:
   - As senhas nunca sÃ£o guardadas em texto plano. SÃ£o hasheadas com SHA-256 e uma chave de salt antes de serem salvas.

---

## ðŸ’¾ Armazenamento & PersistÃªncia de Dados

Todos os registos sÃ£o armazenados no `localStorage` do navegador do cliente:

| Chave | DescriÃ§Ã£o |
|---|---|
| `sdpc_hcn_users` | Cadastro de utilizadores do hospital, departamentos e hashes de senha. |
| `sdpc_hcn_session` | SessÃ£o ativa do profissional conectado. |
| `sdpc_hcn_patients` | ProntuÃ¡rios completos, doentes, formulÃ¡rios F1 a F8, curvas vitais e imagens. |
| `sdpc_appointments` | Fila de marcaÃ§Ãµes efetuadas pelo portal pÃºblico de cidadÃ£os. |

> âš ï¸ **Backup Recomendado**: Use periodicamente a funÃ§Ã£o de exportaÃ§Ã£o de dados (botÃ£o de backup JSON) para salvaguardar os dados dos doentes num dispositivo de armazenamento externo seguro.

---

## ðŸ“Š RelatÃ³rios EstatÃ­sticos & Indicadores de GestÃ£o (TOC)

O sistema inclui um mÃ³dulo de inteligÃªncia hospitalar com cÃ¡lculo oficial da **Taxa de OcupaÃ§Ã£o de Camas (TOC)** do MinistÃ©rio da SaÃºde:

$$\text{TOC (\%)} = \frac{\text{Total de Dias de Internamento do PerÃ­odo}}{\text{Camas DisponÃ­veis} \times \text{Dias do PerÃ­odo}} \times 100$$

- **ClassificaÃ§Ã£o**: Baixa (<50%), Moderada (50-74%), Alta (75-89%) e CrÃ­tica (â‰¥90%).
- **ExportaÃ§Ãµes DisponÃ­veis**:
  - ðŸ“„ **Microsoft Word (.doc)**: RelatÃ³rio formatado com cabeÃ§alho institucional do SNS, tabelas e sÃ­ntese clÃ­nica.
  - ðŸ“Š **Microsoft Excel (.xls)**: Planilha detalhada com listagem nominal de doentes, tempo de internamento e desfechos.
  - ðŸ–¨ï¸ **ImpressÃ£o / PDF**: Layout A4 em alta resoluÃ§Ã£o.

---

## ðŸ“ Estrutura de Ficheiros do Projeto

```text
â”œâ”€â”€ README.md               # DocumentaÃ§Ã£o detalhada e guia de desenvolvimento local
â”œâ”€â”€ sdpc-hcn.html           # Arquivo autÃ³nomo completo do sistema SDPC-HCN
â”œâ”€â”€ metadata.json           # Metadados da aplicaÃ§Ã£o para o ambiente de execuÃ§Ã£o
â”œâ”€â”€ package.json            # ConfiguraÃ§Ã£o de dependÃªncias e scripts de execuÃ§Ã£o
â”œâ”€â”€ tsconfig.json           # ConfiguraÃ§Ãµes do compilador TypeScript
â”œâ”€â”€ vite.config.ts          # ConfiguraÃ§Ã£o do empacotador Vite e Tailwind CSS
â”œâ”€â”€ index.html              # Ponto de entrada web
â”œâ”€â”€ public/
â”‚   â””â”€â”€ sdpc-hcn.html       # CÃ³pia estÃ¡tica servida diretamente pelo servidor web
â””â”€â”€ src/
    â”œâ”€â”€ App.tsx             # AplicaÃ§Ã£o interativa com visualizador do sistema e guia local
    â”œâ”€â”€ main.tsx            # InicializaÃ§Ã£o do React 19
    â””â”€â”€ index.css           # Estilos globais Tailwind
```

---

## â“ SoluÃ§Ã£o de Problemas (Troubleshooting)

- **Os grÃ¡ficos de sinais vitais nÃ£o aparecem**:
  - Verifique se clicou nas cÃ©lulas correspondentes Ã  hora e ao valor de TA, pulso ou temperatura. Ao selecionar ao menos 2 pontos horÃ¡rios, as linhas de evoluÃ§Ã£o sÃ£o traÃ§adas automaticamente.
- **As imagens de Rx e TAC nÃ£o estÃ£o a ser salvas**:
  - Como o armazenamento Ã© no `localStorage` do navegador (limite usual de ~5MB a 10MB por origem), utilize imagens radiogrÃ¡ficas comprimidas ou reduza a resoluÃ§Ã£o antes de anexar.
- **Esqueci a senha do Administrador**:
  - No console do navegador (pressionando `F12` -> aba *Console*), digite:
    ```javascript
    localStorage.removeItem('sdpc_hcn_users');
    localStorage.removeItem('sdpc_hcn_session');
    location.reload();
    ```
    Isso reiniciarÃ¡ os utilizadores e o prÃ³ximo cadastro serÃ¡ o novo administrador.
- **Porta 3000 jÃ¡ em uso (no Vite)**:
  - Altere a porta no comando: `npx vite --port 3001` ou encerre o processo anterior.
