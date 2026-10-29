<div align="center">

<a href="https://github.com/VictorBarros28">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=26&duration=2800&pause=900&color=E11D48&center=true&vCenter=true&width=720&lines=Ol%C3%A1%2C+eu+sou+o+Victor+%F0%9F%91%8B;Automa%C3%A7%C3%A3o+jur%C3%ADdica+em+produ%C3%A7%C3%A3o;Python+%C2%B7+Django+%C2%B7+Celery+%C2%B7+React;Rob%C3%B4s+que+rodam+enquanto+o+escrit%C3%B3rio+dorme" alt="Typing SVG" />
</a>

**Victor Guilherme Barros** · Desenvolvedor Fullstack na [Urbano Vitalino Advogados](https://github.com/Urbano-Vitalino-Advogados) · Engenharia da Computação na Poli/UPE · Recife, PE

<a href="https://www.linkedin.com/in/victorgbarros/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" /></a>
<a href="mailto:victorbarros28@gmail.com"><img src="https://img.shields.io/badge/E--mail-e11d48?style=for-the-badge&logo=gmail&logoColor=white" /></a>
<img src="https://komarev.com/ghpvc/?username=VictorBarros28&style=for-the-badge&color=30363d&label=visitas" />

</div>

---

### `$ whoami`

Há mais de 5 anos construo e mantenho, de ponta a ponta (requisito, código, deploy e sustentação), os **robôs RPA e as integrações** que tiram trabalho repetitivo das mãos de advogados. São cadastros de processos, andamentos, diligências, audiências, prazos e honorários, rodando todo dia contra sistemas jurídicos de clientes, portais de tribunais e o JUS.br.

Meu trabalho vai da raspagem que precisa sobreviver a um login com SSO e TOTP à tela em React onde o operador vê, em tempo real, o que deu certo, o que falhou e por quê.

<div align="center">
  <img src="./assets/terminal.svg" alt="Robô RPA rodando em produção" width="100%" />
</div>

---

### 🗺️ Trajetória

```mermaid
timeline
    2018 : Início de Engenharia da Computação na Poli/UPE
    2020 : Poli Júnior · front-end, sistemas de gestão e e-commerce para pequenas empresas
    2021 : Urbano Vitalino Advogados · primeiros sistemas front-end jurídicos e cadastro cível
    2023-2024 : Robôs de cadastro e andamentos em sistemas de clientes · triagem de publicações com NLP
    2025 : Decisões, honorários e integrações por API · 100+ commits no ano
    2026 : RPA Monitor em tempo real · Central de Andamentos no JUS.br · migração dos robôs para nova plataforma
```

---

### 🧭 Como as peças se encaixam

> Diagrama interativo: dá para ampliar e arrastar direto no GitHub.

```mermaid
flowchart LR
    subgraph Fontes["🌐 Fontes externas"]
        A1[Sistemas jurídicos<br/>dos clientes]
        A2[Portais de tribunais<br/>JUS.br / CNJ]
        A3[E-mails, planilhas<br/>e APIs de parceiros]
    end

    subgraph Robos["🤖 Robôs · Django + Celery"]
        B1[Workers Selenium /<br/>Playwright / CloakBrowser]
        B2[(PostgreSQL)]
        B3[[Redis · filas]]
    end

    subgraph Monitor["📡 RPA Monitor"]
        C1[API Django + DRF]
        C2[Channels · WebSocket]
        C3[Front React + TS]
    end

    A1 & A2 & A3 <--> B1
    B3 --> B1 --> B2
    B1 -- monitor-signals --> C1
    C1 --> C2 --> C3
    C3 -- retentar / conferir na fonte --> C1 --> B3
    B1 -. arquivos .-> S3[(AWS S3)]
```

---

### 🛠️ Projetos que mais me orgulham

<details open>
<summary><b>📡 RPA Monitor</b>: central em tempo real de todas as automações do escritório</summary>
<br/>

Back em **Django + DRF + Channels** e front em **React 19 + TypeScript + Vite + Tailwind + Radix + Framer Motion**. Mais de 20 operações de clientes reportam ali via um pacote interno (`monitor-signals`) que instrumenta cada robô.

- **Conferir na fonte**: compara o volume processado pelo robô com o que existe na origem e explica cada diferença (lançamento tardio, já processado, fora do critério). Virou o padrão de validação das automações.
- **Retentar pelo front**: refaz busca, download e envio para um item ou uma rodada inteira, preservando período e horário da execução original.
- Sincronização automática de planilhas, grupos de acesso por cliente e banner de indisponibilidade quando um portal externo cai.

</details>

<details>
<summary><b>🕷️ Central de Andamentos (SpiderJUS)</b>: crawler de andamentos no JUS.br</summary>
<br/>

Robô em **Playwright + CloakBrowser** que lê andamentos processuais em lote a partir de planilhas, com detecção de bloqueio, paginação, retorno em `.xlsx` e alertas quando a API pública fica instável. Deploy em containers na AWS (ECS).

</details>

<details>
<summary><b>🔐 Robôs que sobrevivem a login hostil</b></summary>
<br/>

Automação de login com **SSO, TOTP (`pyotp`) e passkey/WebAuthn**, renovação de sessão no meio de rodadas longas, captcha e retentativa por item. Quando o login cai, a mensagem diz em qual passo do SSO ele travou.

</details>

<details>
<summary><b>🧯 Caso real: a rodada que morria na sexta hora</b></summary>
<br/>

Uma rodada de ~10 mil andamentos terminava sempre com milhares de itens em `Rodada interrompida`. A causa estava em dois lugares:

1. o robô caía inteiro quando o login falhava 3× seguidas num reinício;
2. o "destrave" do monitor tinha um **teto fixo de 6h** e encerrava rodadas legítimas que ainda devolviam linhas.

A correção foi feita nos dois repositórios: login resiliente com diagnóstico por etapa e um destrave que olha **progresso**, não relógio. Depois disso, os itens foram reprocessados com acompanhamento ao vivo pelo monitor.

</details>

<details>
<summary><b>🧠 Outros</b></summary>
<br/>

- **Publicações**: triagem de publicações jurídicas com NLP (`sentence-transformers`, NLTK) e dados do Redshift.
- **Honorários**: pipeline de faturamento com leitura de e-mail (IMAP), PDFs (PyMuPDF), exportação em XLSX e AWS Lambda.
- **Integrações por API**: cadastro automático de processos entre o sistema do escritório e plataformas de parceiros, com Celery Beat e reprocessamento por data.
- [`simulado-cpa`](https://github.com/VictorBarros28/simulado-cpa): simulado gamificado da certificação CPA da ANBIMA, em um único HTML, com XP e sequências.

</details>

---

### 🧰 Stack do dia a dia

<div align="center">

**Back-end e automação**<br/>
<img src="https://skillicons.dev/icons?i=python,django,redis,postgres,mongodb,selenium&theme=dark" />
<img src="https://img.shields.io/badge/Celery-37814A?style=flat-square&logo=celery&logoColor=white" />
<img src="https://img.shields.io/badge/Playwright-2EAD33?style=flat-square&logo=playwright&logoColor=white" />
<img src="https://img.shields.io/badge/DRF-A30000?style=flat-square&logo=django&logoColor=white" />

**Front-end**<br/>
<img src="https://skillicons.dev/icons?i=react,ts,vite,tailwind,vue&theme=dark" />

**Infra**<br/>
<img src="https://skillicons.dev/icons?i=docker,aws,gcp,kubernetes,linux,githubactions,git&theme=dark" />
<img src="https://img.shields.io/badge/Portainer-13BEF9?style=flat-square&logo=portainer&logoColor=white" />

</div>

---

### 📈 Atividade

<div align="center">

| Ano | Contribuições |
|:---:|:---|
| 2022 | `▍` 21 |
| 2023 | `▌` 28 |
| 2024 | `██▏` 99 |
| 2025 | `███▊` 171 |
| 2026 | `████` 182 *(até outubro)* |

<img src="./profile-3d-contrib/profile-night-rainbow.svg" alt="Contribuições em 3D" width="100%" />

<img src="https://streak-stats.demolab.com?user=VictorBarros28&theme=github-dark-blue&hide_border=true&ring=E11D48&fire=E11D48&currStreakLabel=E11D48&locale=pt_BR" alt="Sequência" />

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/VictorBarros28/VictorBarros28/output/snake-dark.svg" />
  <img alt="Cobrinha comendo as contribuições" src="https://raw.githubusercontent.com/VictorBarros28/VictorBarros28/output/snake.svg" />
</picture>

<sub>A maior parte do meu código vive em repositórios privados da organização. Os gráficos acima contam essas contribuições, mas o código não é público.</sub>

</div>

---

<details>
<summary>🇺🇸 <b>English summary</b></summary>
<br/>

Full-stack developer with 5+ years at a Brazilian law firm, building and running **production RPA and integrations** with Python, Django, Celery, Redis, PostgreSQL, Selenium and Playwright, plus a **real-time monitoring platform** (Django Channels + React/TypeScript) that tracks every automation, reconciles processed volume against the source and lets operators retry from the UI. Computer Engineering student at Poli/UPE, based in Recife, Brazil.

</details>

<div align="center">
<sub>Commits em português, <code>feat:</code> e <code>fix:</code> no começo e o porquê no corpo.</sub>
</div>
