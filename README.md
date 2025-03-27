## Clean Code - Linters

_[PT-BR] only 'cause its a simple college project._

Este repositório foi criado para resolução de exercícios do _Tópico 7 - Linters_ da grade **Clean Code**. [Modelo do Exercício.](https://gitlab.com/professor-rvenson/cleancode-2025-1/-/blob/main/exercicios/exercicio-linters.md?ref_type=heads)

| **Linguagem Sorteada** | **Linter Escolhido** |
|------------------------|----------------------|
| JavaScript             | ESLint               |

### Sobre o Linter

ESLint é a biblioteca de lint para JavaScript/ECMAScript mais utilizada no mercado, criada em 2013 pelo desenvolvedor Nicholas C. Zakas (Yahoo!, Human Who Codes).

Alguns números da ferramenta: 

- 📥 **~50 milhões** de downloads semanais via npm
- 🌟 **25.7k** de _stars_ e **+10k** _issues_ fechadas no GitHub
- 💾 **+10k** commits 

### Instalação

Seguindo a documentação oficial, iremos seguir este tutorial com a instalação da última versão disponível: **v9.23.0**.

#### Pré-Requisitos

**Node.js** (nas versões ^18.18.0, ^20.9.0 ou >=21.1.0) instalado e com suporte a SSL.

_Obs.: caso você esteja usando uma distribuição oficial do Node.js, o SSL sempre estará integrado_.

Arquivo **package.json** criado, para que o setup instale os pacotes corretamente.

```bash
# npm
npm init @eslint/config@latest

# yarn
yarn create @eslint/config

# pnpm
pnpm create @eslint/config@latest

# bun
bun create @eslint/config@latest
```

#### Configuração Inicial

Após rodar o comando acima, serão feitas algumas perguntas para criar o arquivo de configuração com base nas opções selecionadas.

Para este projeto, criaremos um projeto JavaScript _vanilla_ com o seguinte setup: 

![Imagem da configuração utilizada neste projeto](./assets/setup-lint-example.png)

### Integração da Ferramenta
 
#### Regras

O arquivo criado, `esling.config.mjs`, deve estar com essa configuração:

```js
import { defineConfig } from "eslint/config";
import globals from "globals";
import js from "@eslint/js";


export default defineConfig([
  { files: ["**/*.{js,mjs,cjs}"] },
  { files: ["**/*.{js,mjs,cjs}"], languageOptions: { globals: globals.browser } },
  { files: ["**/*.{js,mjs,cjs}"], plugins: { js }, extends: ["js/recommended"] },
]);
```

Podemos então adicionar [Regras](https://eslint.org/docs/latest/rules/), que são o conceito principal da biblioteca: validar se o código atende a uma expectativa e o que fazer caso ele não atenda a mesma. Também podemos estender as configurações com opções adicionais específicas para a regra criada.

**Gravidade das Regras**

- **“off”** ou **0** - desativa a regra
- **“warn”** ou **1** - ativa a regra como um aviso (não afeta o código de saída)
- **“error”** ou **2** - ativa a regra como um erro (o código de saída será 1)

Normalmente, as regras são utilizadas sempre como _error_, para forçar a conformidade do código. Utilize _warn_ caso queira que o ESLint reporte a violação da regra, mas não interrompa nenhum processo. Geralmente utilizamos este método ao inserir uma nova regra que eventualmente será alterada para _error_.

Exemplo: 

```js
import js from "@eslint/js";
import { defineConfig } from "eslint/config";
import globals from "globals";


export default defineConfig([
  { files: ["**/*.{js,mjs,cjs}"] },
  { files: ["**/*.{js,mjs,cjs}"], languageOptions: { globals: globals.browser } },
  { 
    files: ["**/*.{js,mjs,cjs}"],
    plugins: { js }, 
    extends: ["js/recommended"],
    rules: {
      "no-unused-vars": "error",
      "no-undef": "warn",
    },
  },
]);
```

#### Utilização

```bash
# npm (via npx)
npx eslint index.js 

# yarn
yarn dlx eslint index.js 

# pnpm
pnpm dlx eslint index.js 

# bun
bunx eslint index.js 
```

### Automação

### Guias de Estilo

### Regras