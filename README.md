# Construindo-uma-Aplicação-para-Leitura-de-Documentos-Escaneados-com-NodeJS-e-Google-Vision

Neste projeto, exploraremos como criar uma aplicação utilizando Node.js para realizar a leitura de documentos escaneados em PDF utilizando o serviço Google Vision API. O Google Vision API é um serviço de reconhecimento óptico de caracteres (OCR) poderoso que permite extrair texto de imagens e documentos.

#### **1. Introdução**

O Google Vision API oferece recursos avançados para analisar imagens e documentos, incluindo a capacidade de extrair texto de documentos escaneados. Com Node.js, podemos integrar facilmente esse serviço para automatizar a extração de texto de PDFs.

#### **2. Benefícios do Google Vision API**

- **OCR Avançado**: Reconhece texto em diferentes tipos de documentos, incluindo PDFs escaneados.
  
- **API Robusta**: Oferece suporte a vários idiomas e formatos de documentos.
  
- **Integração com Node.js**: SDKs disponíveis para facilitar a integração com aplicações Node.js.

#### **3. Configuração do Ambiente**

Antes de começar, você precisará configurar uma conta no Google Cloud Platform (GCP) para usar o Google Vision API e instalar as dependências necessárias para desenvolver com Node.js.

##### **Módulo 1: Configuração Inicial**

1. **Configuração do Google Cloud Platform (GCP)**:
   
   - Crie um projeto no GCP e habilite a API do Google Vision.
   - Crie uma chave de API para autenticação com o Google Vision.

2. **Instalação do Cliente Google Cloud SDK**:
   
   Instale o pacote `@google-cloud/vision` para utilizar o Google Vision API no Node.js:

   ```bash
   npm install @google-cloud/vision
   ```

3. **Configuração das Credenciais do Google Cloud**:
   
   Configure suas credenciais de serviço para autenticação com o Google Cloud. Isso pode ser feito configurando variáveis de ambiente ou passando diretamente para o cliente Vision.

##### **Módulo 2: Extração de Texto de PDFs Escaneados**

1. **Implementação da Lógica para Leitura de PDFs**:
   
   - Crie um script Node.js para ler PDFs e enviar para o Google Vision API para extração de texto. Aqui está um exemplo:

   ```javascript
   const { createReadStream } = require('fs');
   const { DocumentUnderstandingServiceClient } = require('@google-cloud/documentai').v1;

   async function extractTextFromPDF(filePath) {
       const client = new DocumentUnderstandingServiceClient();

       const request = {
           parent: `projects/${process.env.GOOGLE_PROJECT_ID}/locations/us`,
           inputConfig: {
               content: createReadStream(filePath),
               mimeType: 'application/pdf'
           },
           // Aqui podem ser configuradas outras opções como a linguagem esperada
           // languageHints: ['en'],
       };

       const [result] = await client.processDocument(request);
       const fullText = result.text;

       return fullText;
   }

   // Exemplo de uso
   const pdfPath = 'caminho/para/seu/arquivo.pdf';
   extractTextFromPDF(pdfPath)
       .then(text => console.log('Texto extraído:', text))
       .catch(err => console.error('Erro ao extrair texto:', err));
   ```

   - Este exemplo utiliza a biblioteca `@google-cloud/documentai` para processar o documento PDF e extrair o texto utilizando o Google Vision API.

##### **Módulo 3: Aplicação Completa**

1. **Integração com Outras Funcionalidades**:
   
   - Amplie a aplicação para lidar com múltiplos documentos, armazenamento de resultados em banco de dados, etc.
   - Utilize frameworks como Express.js para criar uma API REST que aceita uploads de PDFs e retorna texto extraído.

2. **Implementação de Interface de Usuário (opcional)**:
   
   - Desenvolva uma interface de usuário simples para permitir uploads de PDFs e exibir resultados de extração.

#### **Conclusão**

Ao seguir este projeto, aprendemos como utilizar o Google Vision API para extrair texto de documentos PDF escaneados usando Node.js de maneira eficiente. A aplicação pode ser expandida para incluir mais funcionalidades conforme necessidade, facilitando a automação de tarefas que envolvem análise de documentos.
