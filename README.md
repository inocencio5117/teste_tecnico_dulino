# Teste técnico Dulino

1) Para lidar com responsividade é imprescindível o uso de media queries e unidades adaptativas como %, rem, vw e vh. Acredito que o uso de pré-processadores, especialmente Scss é muito benéfico pela dinamicidade que ele pode trazer.

    Exemplo:
    
    Link para o codepen: [codepen](https://codepen.io/inocencio5117/pen/rNPPBWw)
    
    ```html
    <div class="container">
      <span class="item-1"></span>
      <span class="item-2"></span>
      <span class="item-3"></span>
    </div>
    ```
    
    ```scss
    .container {
      max-width: 1200px;
      margin: 1rem auto;
      display: grid;
      grid-gap: 1rem;
      width: 100vw;
      height: 100vh;
    
      > span {
        height: 20rem;
        width: 20rem;
      }
    }
    
    .item-1 {
      background-color: #34495e;
    }
    .item-2 {
      background-color: #e74c3c;
    }
    .item-3 {
      background-color: #ffa644;
    }
    
    @media (min-width: 700px) {
      .container {
        grid-template-columns: repeat(2, 1fr);
      }
    }
    
    @media (min-width: 1100px) {
      .container {
        grid-template-columns: repeat(3, 1fr);
      }
    }
    
    ```

#

4) As diferenças entre o `localStorage`, `SessionStorage` e o `IndexedDB` são as seguintes:

    1) localStorage

        * Características:
            - Armazena dados como pares chave-valor
            - Capacidade de armazenamento de até cerca de 5MB de dados.
            - Dados persistem até mesmo após o fechamento do navegador.

        * Casos de uso:
            - Configuração do usuário.
            - Preferências de interface.
            - Dados que podem ser compartilhados entre sessões.

        * Considerações e limitações:
            - Os dados armazenados são acessíveis por qualquer script na mesma origem.
            - Limite de armazenamento (cerca de 5MB) pode ser uma restrição.
            - Dados são armazenados como strings, então a serialização/desserialização pode ser necessária.

        * Exemplo de uso:
            ```js
            localStorage.setItem('userSettings', JSON.stringify({ theme: 'dark', language: 'en' }));

            const userSettings = JSON.parse(localStorage.getItem('userSettings'));

            ```

        ##

    2) sessionStorage:

        * Características:
            - Semelhante ao localStorage, mas os dados persistem apenas durante a sessão do navegador.
            - Os dados são removidos quando a guia ou janela é fechada.

        * Casos de Uso:
            - Dados temporários que não precisam ser mantidos entre sessões.
            - Informações temporárias necessárias durante uma única sessão.

        * Considerações e Limitações:
            - Limite de armazenamento semelhante ao localStorage (cerca de 5MB).
            - Dados são acessíveis apenas durante a sessão atual.

        * Exemplo de uso:
            ```js
            sessionStorage.setItem('temporaryData', 'someValue');

            const temporaryData = sessionStorage.getItem('temporaryData');

            ```

        ##

    3) IndexedDB:

        * Características:
            - Banco de dados NoSQL no lado do cliente.
            - Suporta armazenamento de grandes volumes de dados.
            - Permite operações assíncronas.

        * Casos de Uso:
            - Armazenamento de dados estruturados e complexos.
            - Grandes conjuntos de dados que podem ser consultados.

        * Considerações e Limitações:
            - Mais complexo de implementar em comparação com localStorage e sessionStorage.
            - Suporte para transações, permitindo operações atômicas.
            - Pode ser exagerado para casos simples.

        * Exemplo de uso:
            ```js
            const db = window.indexedDB.open('userDatabase', 1);

            db.onupgradeneeded = (event) => {
            const database = event.target.result;
            const objectStore = database.createObjectStore('users', { keyPath: 'id' });
            };

            const transaction = db.transaction(['users'], 'readwrite');
            const objectStore = transaction.objectStore('users');
            objectStore.add({ id: 1, name: 'John Doe', age: 30 });

            ```
