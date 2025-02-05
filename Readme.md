![poster](./.github/poster.png)

## Sobre

Repositório do treinamento: Workflow de testes contínuos em Cypress no Github Actions

## Stacks
- Cypress
- Javascript
- Cypress Dashboard
- Tesults

## Rodando

1. Clonar o repositório, instalar as dependências
```
yarn / npm install
```

2. Subir o Cypress UI
```
yarn cypress open / npx cypress open 
```

3. Executar testes em Headless
```
yarn cypress run / npx cypress run 
```

<hr>
Curso disponível em https://qaxperience.com


4. Instalar Allure

- habilitar o yarn
corepack enable

- Install Allure
yarn add -D @shelex/cypress-allure-plugin

- Access the config file and update:
- Copy the rows with arrows to the config file:

>> const allureWriter = require('@shelex/cypress-allure-plugin/writer');
// import allureWriter from "@shelex/cypress-allure-plugin/writer";

module.exports = defineConfig({
    e2e: {
        setupNodeEvents(on, config) {
    >>      allureWriter(on, config);
    >>      return config;
        }
    }
});

- Copy this row to the "e2e.js" file:
require('@shelex/cypress-allure-plugin');

- to enable the generation of the report after the test execution copy this row:
npx cypress run --env allure=true
- Obs.: The results will be generated in json file. To generate the report one more step is needed.

- install the CLI from report allure:
yarn add -D allure-commandline

- after the installation, type the line below that will read the allure results folder and create the local server for report
>> npx allure serve

- Obs.: If a message "ERROR": JAVA_HOME is not set and no 'java' command could be found in your PATH.
>> The JAVA must be installed on the machine. Download the JDK from JAVA. MSI installer (Java Development Kit) in this way JRE wil be installed in the same package(Java Runtim Environment).
>> the go to c:\ProgramFiles\Java\jdk-20 >> copy this adress 
>> open computer properties >> advanced system settings >> Environment Variables >> System Variables >> add a variable >> Name will be "JAVA_HOME" and the Variabe value "c:\ProgramFiles\Java\jdk-20" >> Save.

- Inform this row in the cypress.config.js. This will allow to type only "npx cypress run" to run the tests and generate the allure report.
- the row "allureAddVideoOnPass: true" will save the videos that have passed on the allure report.
    env: {
      allure: true,
      allureAddVideoOnPass: true 
    },

- It will read the folder allure results and generate the report o html and generate a folder allure report.
>> npx allure generate
- to access this folder we need to have a web server. Put this into a web server. Steps below.

- Install a package to run a http server wherever I want on my computer
>>  yarn add -D http-server
>> access the allure folder
>> go to the root of project "cypress-actions-allure"
>> npx http-server allure-report/
- this will run the http server on the folder allure report
>> localhost:8080 >> to access the allure report

- add the rows below to the gitignore
allure-report
allure-results

Obs.: On the company ask for a http server to the infra to keep al the report online. Serch for the platform like azure, ec2, amazon cloud, cloud datacenter, not paying service.