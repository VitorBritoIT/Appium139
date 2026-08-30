Este repositório documenta a implementação de testes automatizados mobile utilizando o ecossistema **.NET (C#)** integrado ao **Appium** e **NUnit**, executando testes em nuvem através do **Sauce Labs** com foco no aplicativo demonstrativo **My Demo App (Android)**.

---

🎯 Objetivo & Foco do Projeto

Validação funcional ponta a ponta (E2E) do fluxo de seleção e adição de produtos ao carrinho no aplicativo Android (*My Demo App*), cobrindo desde a configuração de capabilities em nuvem até a manipulação de gestos de tela e asserções de integridade de dados.

🔹 Destaques Técnicos do Código
- **Execução Cloud (Sauce Labs):** Configuração de sessão remota autenticada via variáveis de ambiente (`SAUCE_USERNAME` e `SAUCE_ACCESS_KEY`).
- **AppiumOptions & Capabilities:** Definição de plataforma Android, emulador Samsung Galaxy S9 (API 9.0), `appPackage`, `appActivity` e gerenciamento de timeouts (`newCommandTimeout` e `commandTimeout`).
- **Localização de Elementos Mobile:** Uso de seletores nativos via `MobileBy.AccessibilityId` e `MobileBy.Id`.
- **Gestos de Tela (TouchAction):** Implementação de scroll manual (*swipe up*) utilizando coordenadas (`Press`, `MoveTo`, `Release`, `Perform`) para alcançar botões fora da área visível.
- **Validações & Asserções:** Validação de exibição do logo inicial, nome do produto e preço unitário tanto na tela de detalhes quanto dentro do carrinho (`cartTV`).

---

🧪 Fluxo de Teste Automatizado (`SelectProductMDA`)

1. **Setup (`[SetUp]`):** Inicialização do `AndroidDriver<AndroidElement>` apontando para o hub da Sauce Labs com o binário `mda-2.0.0-21.apk`.
2. **Validação Inicial:** Confirmação de carregamento da Home (`App logo and name`).
3. **Seleção de Produto:** Clique no item *Sauce Labs Backpack*.
4. **Validação de Detalhes:** Asserção do título (`productTV`) e preço (`$ 29.99` em `priceTV`).
5. **Ação de Scroll:** Deslocamento vertical de tela via `TouchAction` para visualização do botão de compra.
6. **Adição ao Carrinho:** Clique em *Tap to add product to cart* e navegação para o carrinho (`cartTV`).
7. **Validação no Carrinho:** Confirmação do título (`titleTV`) e preço final do produto adicionado.
8. **TearDown (`[TearDown]`):** Finalização da sessão com `driver.Quit()` e liberação de recursos (`driver.Dispose()`).

---

Estrutura do Projeto

```
Appium139/
├── SelectProductMDA.cs    # Classe de teste NUnit com o fluxo E2E no app Android
├── appium.csproj          # Configurações do projeto .NET e dependências NuGet
└── README.md              # Documentação do projeto
