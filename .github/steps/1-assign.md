
## Etapa 1: Habilite o agente de código Copilot

No exercício [Primeiros Passos com o GitHub Copilot](/skills/getting-started-with-github-copilot), aprendemos como usar o Copilot no editor de código para fazer grandes melhorias no site de Atividades Extracurriculares da Escola Mergington. 🎻 ⚽️ ♟️

Na verdade, o site se tornou uma ferramenta regular da escola. E, embora você goste dessa atenção, percebeu um problema! Você está prestes a sair de licença no próximo semestre!

Após conversar com a direção, eles aceitaram que novas funcionalidades podem esperar, mas... ficaram preocupados. É preciso ter _algo_ para lidar com pequenas mudanças enquanto você estiver ausente.

Vamos preparar os professores para o sucesso, cadastrando o Copilot (na nossa escola) para cuidar das atualizações enquanto estivermos fora.

<img width="600" alt="screenshot do WebApp da Escola Mergington" src="https://github.com/user-attachments/assets/6f5c59ab-398b-4fb0-8efd-0aa7b72fef97" />

### O Copilot agora é seu agente de código!

Em exercícios anteriores, usamos o Copilot em **chat**, **edições** e modo **agente**. Embora esses modos sejam úteis, o **agente de código Copilot** leva isso a outro nível, operando totalmente pelo GitHub. Não precisa de editor de código! 😎

| Recurso           | Copilot no editor             | Agente de código Copilot |
| ----------------- | ----------------------------- | ------------------------ |
| **Interface**     | Seu editor de código          | Issues e Pull Requests   |
| **Escopo**        | Arquivos locais               | Repositório              |
| **Ativação**      | Sugestões inline, chat        | Atribuição de issue      |
| **Customização**  | Instruções personalizadas     | Instruções personalizadas|
| **Suporte MCP**   | Sim                          | Sim                      |
| **Vibe Coding**   | 😎                            | 😎                       |

### Como funciona?

Do ponto de vista do colaborador, o fluxo é muito parecido com o de um projeto normal.

1. Um colaborador com **acesso de escrita** seleciona uma issue e a atribui ao Copilot (em vez de si mesmo).
2. O Copilot cria um branch e um pull request.
3. O Copilot trabalha no branch em um workflow do Actions e fornece atualizações na aba de conversas do pull request.
4. Quando o Copilot termina a issue, quem atribuiu é solicitado a revisar.
5. O responsável faz a revisão, adiciona comentários ou aprova.
6. Se houver feedback, o Copilot continua trabalhando para implementar as sugestões.
7. O solicitante repete os passos acima até ficar satisfeito e então faz o merge.

```mermaid
flowchart LR

    contributor((Contributor))
    copilot((Copilot))
    reviewer((Reviewer))

    issue@{ shape: notch-rect, label: "Issue" }
    repo@{ shape: cyl, label: "Repository" }
    branch@{ shape: subproc, label: "Branch" }
    review@{ shape: diamond, label: "Review" }


    subgraph PR[Pull Request]
        direction TB
        branch
        review
        reviewer
    end


    %% Assign
    contributor gl1@-->|Selects| issue
    issue gl2@-->|Assigns to| copilot

    %% Work
    copilot pl1@-->|Creates| branch
    branch pl3@-->|Starts| review

    %% Review
    reviewer gl3@-->|Provides feedback| review
    review pl4@--> |Implements feedback| branch

    %% Approved
    review gl4@-->|Approves and merges| repo


    classDef users fill:#08872B,stroke:#5FED83,color:#fff
    classDef repo fill:#08872B,stroke:#5FED83,color:#fff
    classDef agent fill:#501DAF,stroke:#C06EFF,color:#fff
    classDef pr fill:#0969DA,stroke:#0349B4,color:#fff

    classDef green-line stroke:#08872B, stroke-width:4px;
    classDef purple-line stroke:#501DAF, stroke-width:4px;

    class contributor,reviewer users
    class copilot agent
    class repo repo

    class gl1,gl2,gl3,gl4 green-line
    class pl1,pl2,pl3,pl4 purple-line
```

### Is this safe?

Several security precautions have been implemented to help reduce concerns. Here are a few limitations that you might need to consider when asking Copilot to work on an issue.

- Copilot can only make changes on the branch it created and resources provided by the repository.
- Copilot has [configurable firewall](https://docs.github.com/en/enterprise-cloud@latest/early-access/copilot/coding-agent/customizing-copilot-coding-agents-development-environment#customizing-or-disabling-the-agents-firewall) that restricts access to the internet.
- Only users with write access can assign Copilot an issue.
- Hidden content in issues (like commented code) is ignored.

> [!IMPORTANT]
> The full list of mitigations and configuration settings can be found in the [Risks & Mitigations](https://docs.github.com/en/enterprise-cloud@latest/early-access/copilot/coding-agent/using-copilot-coding-agent#copilot-coding-agent-risks-and-mitigations) documentation.

## ⌨️ Activity: (optional) Get to know our extracurricular activities site

> [!NOTE]
> Opening a development environment and running the application is not necessary to complete this exercise. You can skip this activity if desired.

<details>
<summary>Show Steps</summary>

In other exercises, we have been developing the Extracurricular Activities website. You can follow these steps to start up the development environment and try it out.

1. Right-click the below button to open the **Create Codespace** page in a new tab. Use the default configuration.

   [![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/{{full_repo_name}}?quickstart=1)

1. Wait some time for the environment to be prepared. It will automatically install all requirements and services.

1. Validate the **GitHub Copilot** and **Python** extensions are installed and enabled.

   <img width="300" alt="copilot extension for VS Code" src="https://github.com/user-attachments/assets/ef1ef984-17fc-4b20-a9a6-65a866def468" /><br/>
   <img width="300" alt="python extension for VS Code" src="https://github.com/user-attachments/assets/3040c0f5-1658-47e2-a439-20504a384f77" />

1. Try running the the application. In the left sidebar, select the **Run and Debug** tab and then press the **Start Debugging** icon.

   <details>
   <summary>📸 Show screenshot</summary><br/>

   <img width="300" alt="run and debug" src="https://github.com/user-attachments/assets/50b27f2a-5eab-4827-9343-ab5bce62357e" />

   </details>

   <details>
   <summary>🤷 Having trouble?</summary><br/>

   If the **Run and Debug** area is empty, try reloading VS Code: Open the command palette (`Ctrl`+`Shift`+`P`) and search for `Developer: Reload Window`.

   <img width="300" alt="empty run and debug panel" src="https://github.com/user-attachments/assets/0dbf1407-3a97-401a-a630-f462697082d6" />

   </details>

1. Use the **Ports** tab to find the webpage address, open it, and verify it is running.

   <details>
   <summary>📸 Show screenshot</summary><br/>

   <img width="350" alt="ports tab" src="https://github.com/user-attachments/assets/8d24d6b5-202d-4109-8174-2f0d1e4d8d44" />

   </details>

</details>

## ⌨️ Activity: Enable Copilot coding agent on your repository

Before we can start delegating requests from the teachers to Copilot, we need to grant access to our repository.

1. In the top right, click your **user icon** and select **Settings**.

   <img width="300" src="https://github.com/user-attachments/assets/7f8c3602-6de2-4c75-8047-8f4853495f46"><br/>
   <img width="300" src="https://github.com/user-attachments/assets/2aedfd6e-8b9f-40bb-bdf9-c9fd597f94a4">

1. In the left navigation, expand the **Copilot** section and select **Coding agent**.

   <img width="300" src="https://github.com/user-attachments/assets/79800990-6d5c-4055-acc9-b15734fe8b80">

1. Change the **Repository access** field to `Only selected repositories`.

   <img width="300" src="https://github.com/user-attachments/assets/7a665042-b064-4baf-a7e7-0dfc0261063e">

1. Click the **Select repositories** button and ensure this exercise is select.

   <img width="300" src="https://github.com/user-attachments/assets/4bec16dc-7b52-4e95-b554-47252b622adb">

## ⌨️ Activity: Assign Copilot an issue

There are several important issues to get done before we leave, but let's do a test run on one of the simple options first. This will let us see how interactions and collaboration work, so we can update our docs for guiding the other teachers. Most don't know how to use a traditional coding editor!

> [!TIP]
> Try to make an issue's goal and acceptance criteria clear. Also, breaking down large tasks into shorter ones provides more opportunity for feedback!

1. Return to your [exercise repository](<(https://github.com/{{full_repo_name}})>).

1. In the top navigation, select the **Issues** tab.

1. Above the list, on the top right, click the **New Issue** button.

1. Set the **Title** to:

   ```md
   Missing Activity: Manga Maniacs
   ```

   Enter the below text as description, and click the **Create** button.

   ```md
   The manga club was recently announced and is naturally missing from the website. Please add it.

   Here are the details:

   Description: Explore the fantastic stories of the most interesting characters from Japanese Manga (graphic novels).

   Schedule: Tuesdays at 7pm
   Max attendance: 15 people
   ```

1. In the top right, click on the **Assignees** area and select **Copilot**.

   <img width="350" src="https://github.com/user-attachments/assets/444f9432-17c3-4466-bb8e-aa4e44238130" />

1. At the bottom, click the **Create** button. After a moment, you will notice:

   - The issue will have an `👀` reaction to show Copilot is reading the issue.
   - The activity log shows you assigned the issue to Copilot.
   - The issue log includes a linked pull request.

   <img width="350" src="https://github.com/user-attachments/assets/40245540-e717-43b3-b2be-90f25cc494d0" />

1. With the issue assigned, Mona should be busy checking your work. Give her a moment to share the next steps.

<details>
   <summary>Having trouble? 🤷</summary><br/>

If you don't get feedback, here are some things to check:

- Make sure you assigned the correct issue. If you practice on other issues, they will be ignored.

</details>
