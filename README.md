<!-- NPM / Yarn -->
npm install vue@latest

## Hooks do Ciclo de Vida do Vue 3:
setup: Este não é um hook de ciclo de vida no sentido tradicional, mas sim uma função especial usada na Composition API para configurar o componente. É aqui que você define a lógica do componente, como estado reativo, computações, ações, etc. A função setup é executada antes de outros hooks do ciclo de vida.

beforeCreate: Executado imediatamente após a instância do componente ser criada. Nesse ponto, as opções do componente ainda não foram processadas.

created: Executado após a instância do componente ser criada. As opções do componente já foram processadas, e os dados reativos, computadas e métodos são configurados. No entanto, o componente ainda não foi montado no DOM.

beforeMount: Executado antes do componente ser montado no DOM. Neste ponto, o template do componente foi compilado, mas ainda não foi renderizado no DOM.

mounted: Executado após o componente ser montado no DOM. Neste ponto, o template do componente foi renderizado e o componente está disponível no DOM. É um bom lugar para interações com a DOM ou para executar operações que dependem do componente estar visível no DOM.

beforeUpdate: Executado antes do componente ser atualizado no DOM devido a mudanças de dados. Este hook é acionado quando os dados reativos do componente são alterados, mas antes do componente ser renderizado novamente no DOM.

updated: Executado após o componente ser atualizado no DOM devido a mudanças de dados. Neste ponto, o componente foi re-renderizado no DOM com base nas alterações nos dados reativos.

beforeUnmount: Executado antes do componente ser desmontado e destruído. É um bom lugar para limpar recursos, desconectar eventos ou realizar outras tarefas de limpeza.

unmounted: Executado após o componente ser desmontado e destruído. Neste ponto, o componente não está mais presente no DOM e foi completamente desativado.

## Ciclo de Vida do Vue - Visão Geral:
Criação: O ciclo de vida começa com a criação da instância do componente. Nesse estágio, o Vue instancia o componente, mas ainda não processa suas opções (como dados, métodos e hooks).

beforeCreate: Este é o primeiro hook a ser acionado. Neste ponto, o componente existe, mas suas opções ainda não foram processadas.

created: Após o processamento das opções do componente, o hook created é acionado. Neste ponto, os dados reativos, computadas e métodos do componente são configurados.

Montagem: Depois que o componente é criado, ele precisa ser montado no DOM.

beforeMount: Neste ponto, o template do componente foi compilado, mas ainda não foi renderizado no DOM.

mounted: Após a renderização do template do componente no DOM, o hook mounted é acionado. Agora o componente está disponível no DOM e pode ser interagido.

Atualização: Quando os dados reativos do componente são alterados, o componente precisa ser atualizado no DOM para refletir essas mudanças.

beforeUpdate: Antes que o componente seja atualizado no DOM, o hook beforeUpdate é acionado.

updated: Após a atualização do componente no DOM, o hook updated é acionado. Neste ponto, o componente foi re-renderizado no DOM com base nas alterações nos dados reativos.

Desmontagem: Quando o componente não é mais necessário, ele é desmontado e destruído.

beforeUnmount: Antes do componente ser desmontado, o hook beforeUnmount é acionado. É um bom lugar para limpar recursos, desconectar eventos ou realizar outras tarefas de limpeza.

unmounted: Após o desmonte do componente, o hook unmounted é acionado. Neste ponto, o componente não está mais presente no DOM e foi completamente desativado.

Entender o ciclo de vida do Vue é fundamental para gerenciar o comportamento do componente em diferentes estágios de sua existência. O Vue 3 trouxe algumas mudanças nos nomes dos hooks em relação ao Vue 2, mas o conceito geral do ciclo de vida permanece o mesmo. Com a ajuda da Composition API e do hook setup, é possível ter um controle mais granular sobre a lógica e o comportamento do componente em cada estágio do ciclo de vida.

## Watchers:
Em Vue.js, o "Watchers" é um recurso que permite que você reaja às mudanças nos dados reativos do componente e realize ações específicas quando essas mudanças ocorrem. O watch() é uma função que você pode usar para criar um observador que ficará "observando" uma expressão reativa e executará uma função de callback sempre que essa expressão for modificada.

Sintaxe do watch():
`
watch(
  // Expressão a ser observada (pode ser uma função computada, uma propriedade reativa ou uma função que retorna um valor reativo)
  expression,

  // Função de callback que será executada quando a expressão mudar
  (newValue, oldValue) => {
    // Ação a ser realizada com o novo valor (newValue) e o valor anterior (oldValue)
  },

  // Opções (opcional)
  {
    // deep: boolean - Monitorar alterações profundas em objetos e arrays (padrão: false)
    // immediate: boolean - Executar a função de callback imediatamente após a criação do observador (padrão: false)
  }
);
`
### Usabilidade do watch():
O watch() é útil quando você precisa executar lógica complexa ou reativa em resposta a alterações específicas nos dados do componente. Algumas situações em que o watch() pode ser usado incluem:

Observar Mudanças em Propriedades Reactivas:
Você pode usar o watch() para monitorar alterações em propriedades reativas do componente e, assim, executar ações específicas com base nessas alterações. Por exemplo, atualizar um gráfico sempre que os dados que o alimentam mudarem.

Ações Dependentes de Várias Propriedades:
Em alguns cenários, você pode precisar realizar ações com base na interação entre várias propriedades reativas. Com o watch(), você pode observar várias expressões reativas e desencadear ações quando qualquer uma delas mudar.

Observar Alterações em Dados Assíncronos:
Se você tiver dados assíncronos que podem ser alterados após uma chamada de API ou carregamento dinâmico, o watch() pode ser útil para reagir a essas mudanças e atualizar a interface do usuário de acordo.

Realizar Ações de Limpeza:
Em alguns casos, você pode precisar executar ações de limpeza ou liberação de recursos quando uma propriedade reativa específica for alterada ou quando o componente for desmontado. O watch() pode ser usado para realizar essas ações antes ou depois das mudanças.

## Exemplo de uso do `watch()`:
`
<template>
  <div>
    <p>Contador: {{ counter }}</p>
    <button @click="increment">Incrementar</button>
  </div>
</template>

<script>
import { reactive, watch } from 'vue';

export default {
  setup() {
    const state = reactive({
      counter: 0,
    });

    const increment = () => {
      state.counter++;
    };

    // Observando a mudança na propriedade "counter"
    watch(
      () => state.counter,
      (newValue, oldValue) => {
        console.log(`Valor anterior: ${oldValue}, Novo valor: ${newValue}`);
        // Outras ações baseadas na mudança do contador podem ser realizadas aqui
      }
    );

    return {
      counter: state.counter,
      increment,
    };
  },
};
</script>
`

No Vue 3, a diretiva computed foi substituída pela função computed() da Composition API. O computed() é um recurso que permite criar propriedades reativas que dependem de outros dados reativos. Essas propriedades computadas são calculadas automaticamente pelo Vue e atualizadas somente quando suas dependências são modificadas.

### Sintaxe do computed():
`
import { computed } from 'vue';

const myComputedProperty = computed(() => {
  // Lógica computada baseada em outras propriedades reativas
  return someReactiveData.value + anotherReactiveData.value;
});
`
### Aplicabilidade do computed():
O computed() é útil quando você precisa realizar cálculos ou transformações com base em propriedades reativas existentes. Ele ajuda a manter a lógica reativa organizada e facilita o desenvolvimento de interfaces de usuário responsivas. Alguns casos comuns de aplicação do computed() são:

### Manipulação e Combinação de Dados:
Se você precisar combinar ou manipular várias propriedades reativas para obter um resultado específico, o computed() é uma escolha adequada. Por exemplo, calcular o total de um carrinho de compras com base nos preços e quantidades dos itens.

### Formatação de Dados:
Para exibir informações de maneira formatada ou estilizada, o computed() é útil. Por exemplo, formatar datas ou valores monetários para uma exibição mais amigável.

### Filtragem e Classificação de Dados:
Ao filtrar ou classificar uma lista de itens com base em certos critérios, o computed() pode ser usado para criar uma propriedade reativa com os itens filtrados ou classificados.

### Validação de Entradas:
No caso de validação de entradas de formulário, o computed() pode ser empregado para verificar se os campos atendem a determinados critérios e gerar mensagens de erro dinâmicas.

### Exemplo de uso do computed():
`
<template>
  <div>
    <p>Preço do Item: {{ price }}</p>
    <p>Quantidade: <input v-model="quantity" type="number"></p>
    <p>Total: {{ total }}</p>
  </div>
</template>

<script>
import { ref, computed } from 'vue';

export default {
  setup() {
    const price = ref(10);
    const quantity = ref(1);

    // Criação da propriedade computada "total"
    const total = computed(() => {
      return price.value * quantity.value;
    });

    return {
      price,
      quantity,
      total,
    };
  },
};
</script>
`
Neste exemplo, criamos uma propriedade reativa price e uma propriedade reativa quantity, representando o preço e a quantidade de um item, respectivamente. Usando o computed(), definimos a propriedade computada total, que depende dos valores de price e quantity. Sempre que o preço ou a quantidade for alterada, o Vue automaticamente recalculará o valor da propriedade total.

Em resumo, o computed() é uma maneira eficiente de criar propriedades reativas derivadas de outras propriedades reativas, evitando redundâncias de cálculos e mantendo a interface do usuário atualizada de forma reativa. Ele é particularmente útil para cálculos e formatações complexas que dependem de dados reativos e devem ser atualizados automaticamente quando esses dados mudam.

O Vue 3 oferece duas formas principais de criar dados reativos: ref e reactive. Ambas são importantes na Composition API e têm diferentes aplicabilidades, dependendo do cenário em que são utilizadas.

### ref:
A função ref é usada para criar um dado reativo para valores primitivos, como números, strings e booleanos. O ref encapsula o valor em um objeto especial com a propriedade value, e esse objeto reativo pode ser modificado diretamente ou através da propriedade value. Ele é especialmente útil quando você precisa reagir às mudanças de um valor primitivo em um componente Vue.

### Aplicabilidade do ref:
Valores Primitivos:
O ref é mais adequado para valores primitivos, como números, strings e booleanos, pois cria uma referência reativa a esse valor. Por exemplo, contadores, flags de controle ou valores de entrada do usuário.

### Valores Iniciais:
Quando você precisa definir um valor inicial para um dado reativo, o ref é uma boa escolha. É comum utilizá-lo para inicializar valores antes de serem reativos.

### Interligação com Formulários:
O ref pode ser útil para interligar valores de formulários com v-model, pois garante que as mudanças nos elementos de formulário reflitam imediatamente nas propriedades reativas.

### reactive:
A função reactive é usada para criar um objeto reativo que contém propriedades reativas. Essas propriedades podem ser objetos ou arrays, e qualquer alteração em uma dessas propriedades será rastreada pelo Vue. O reactive é ideal para lidar com estados complexos e estruturas de dados mais avançadas.

### Aplicabilidade do reactive:
Objetos e Arrays Complexos:
O reactive é mais adequado para criar objetos ou arrays complexos, pois permite que você crie um objeto reativo que contém várias propriedades reativas. Por exemplo, estado global da aplicação, listas de itens e formulários complexos.

### Composição de Estado:
Quando você precisa compor um estado mais avançado, com diversas propriedades reativas em um único objeto, o reactive é uma ótima opção.

### Gerenciadores de Estado:
O reactive é muito usado em gerenciadores de estado, como o Vuex ou o Pinia, para criar o estado global da aplicação e reagir às mudanças de estado.

## Exemplo de Uso de ref e reactive:
`
<template>
  <div>
    <p>Counter: {{ counter.value }}</p>
    <button @click="increment">Increment</button>
  </div>
</template>

<script>
import { ref, reactive } from 'vue';

export default {
  setup() {
    // Exemplo de uso do ref para um contador simples
    const counter = ref(0);

    // Exemplo de uso do reactive para um estado mais complexo
    const state = reactive({
      username: 'user',
      age: 25,
      todos: [],
    });

    const increment = () => {
      counter.value++;
    };

    return {
      counter,
      state,
      increment,
    };
  },
};
</script>
`
Neste exemplo, utilizamos ref para criar o counter, que é um simples valor numérico, e reactive para criar o state, que é um objeto reativo com propriedades username, age e todos.

Em resumo, ref é usado para criar dados reativos de valores primitivos e reactive é usado para criar objetos reativos que contêm propriedades reativas. Escolha a abordagem adequada ao lidar com diferentes tipos de dados e requisitos de estado na sua aplicação Vue 3.

## Pinia
O Pinia é um gerenciador de estado oficialmente recomendado pelo Vue.js para aplicações Vue 3. Ele oferece uma abordagem simples, flexível e escalável para gerenciar o estado da aplicação, especialmente em projetos maiores e complexos. O Pinia é baseado na Composition API e utiliza as funcionalidades mais recentes do Vue 3.

Aplicabilidade do Pinia:
O Pinia é recomendado principalmente para aplicações Vue 3 que possuam:

Complexidade Crescente: Conforme sua aplicação cresce, a complexidade do gerenciamento de estado aumenta. O Pinia oferece uma estrutura organizada para lidar com o estado global de forma mais eficiente.

Múltiplos Componentes Reativos: Quando vários componentes precisam compartilhar o mesmo estado, o Pinia facilita o compartilhamento do estado e a comunicação entre componentes de maneira mais clara e estruturada.

Composable Functions: O Pinia facilita a criação de funções componíveis (composable functions) que encapsulam a lógica de acesso e mutação do estado, promovendo uma melhor modularidade e reutilização do código.

Respeito à Flux Arquitetura: Para projetos que preferem seguir uma arquitetura flux ou similar, o Pinia se integra naturalmente, permitindo a criação de stores (armazéns) que são mais previsíveis e independentes.

Exemplos Práticos de Uso do Pinia:
Exemplo 1: Contador Global:
`
<!-- main.js -->
import { createPinia } from 'pinia';
import { createApp } from 'vue';
import App from './App.vue';

const pinia = createPinia();

createApp(App).use(pinia).mount('#app');
`
`
<!-- store/counter.js -->
import { defineStore } from 'pinia';

export const useCounterStore = defineStore({
  id: 'counter',
  state: () => ({
    count: 0,
  }),
  actions: {
    increment() {
      this.count++;
    },
    decrement() {
      this.count--;
    },
  },
});
`
`
<!-- components/Counter.vue -->
<template>
  <div>
    <p>Contador: {{ counter }}</p>
    <button @click="increment">Incrementar</button>
    <button @click="decrement">Decrementar</button>
  </div>
</template>

<script>
import { useCounterStore } from '../store/counter';

export default {
  setup() {
    const counterStore = useCounterStore();

    return {
      counter: counterStore.count,
      increment: counterStore.increment,
      decrement: counterStore.decrement,
    };
  },
};
</script>
`
Neste exemplo, criamos um contador global utilizando o Pinia. O estado do contador é gerenciado pelo useCounterStore, que define as propriedades reativas count e as ações increment e decrement. Os componentes têm acesso ao contador global utilizando o useCounterStore, que é compartilhado entre todos os componentes.

Exemplo 2: Lista de Tarefas:
`
<!-- store/todo.js -->
import { defineStore } from 'pinia';

export const useTodoStore = defineStore({
  id: 'todo',
  state: () => ({
    todos: [],
  }),
  actions: {
    addTodo(todo) {
      this.todos.push(todo);
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
  },
});
`
`
<!-- components/TodoList.vue -->
<template>
  <div>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        {{ todo }}
        <button @click="removeTodo(index)">Remover</button>
      </li>
    </ul>
    <input v-model="newTodo" @keyup.enter="addTodo">
    <button @click="addTodo">Adicionar</button>
  </div>
</template>

<script>
import { useTodoStore } from '../store/todo';

export default {
  setup() {
    const todoStore = useTodoStore();

    return {
      todos: todoStore.todos,
      newTodo: '',
      addTodo() {
        if (this.newTodo.trim() !== '') {
          todoStore.addTodo(this.newTodo);
          this.newTodo = '';
        }
      },
      removeTodo: todoStore.removeTodo,
    };
  },
};
</script>
`
Neste exemplo, utilizamos o Pinia para criar um gerenciador de estado para uma lista de tarefas. O useTodoStore gerencia o estado da lista de tarefas, que é compartilhado entre todos os componentes. O componente TodoList utiliza as ações addTodo e removeTodo do store para adicionar e remover tarefas da lista.

## Por que Usar um Gerenciador de Estado como o Pinia?
Utilizar um gerenciador de estado, como o Pinia, proporciona uma série de benefícios:

### Centralização do Estado:
Com um gerenciador de estado, todo o estado global da aplicação fica centralizado em stores, facilitando a organização e o entendimento do fluxo dos dados.

### Reatividade:
O Pinia é baseado no sistema de reatividade do Vue 3, garantindo que as mudanças no estado sejam refletidas automaticamente em todos os componentes que o utilizam.

### Modularidade:
Cada store representa um pedaço específico do estado da aplicação, tornando mais fácil adicionar, modificar e reutilizar lógicas relacionadas.

### Gerenciamento Eficiente:
Com um gerenciador de estado, é possível definir ações que realizam operações complexas ou assíncronas e compartilhar essas ações entre componentes.

### Desacoplamento de Componentes:
Os componentes não precisam se preocupar com a obtenção e manipulação direta do estado global. Eles podem simplesmente utilizar as ações do store, deixando a lógica reativa mais isolada e focada.

Em projetos maiores ou com necessidades de gerenciamento de estado mais complexas, o uso de um gerenciador de estado, como o Pinia, pode levar a uma estrutura mais organizada e manutenível, tornando o desenvolvimento de aplicações Vue 3 mais eficiente e escalável.

## Vue Router
O Vue Router é o roteador oficial para aplicações Vue.js. Ele é um componente fundamental para a construção de Single Page Applications (SPAs) e aplicações com múltiplas páginas. O Vue Router é baseado na Composition API e utiliza as funcionalidades mais recentes do Vue 3.

### Aplicabilidade do Vue Router:
O Vue Router é recomendado principalmente para aplicações Vue 3 que possuam:

### Múltiplas Páginas:
Quando você precisa de múltiplas páginas em sua aplicação, o Vue Router é uma ótima opção para gerenciar as rotas e a navegação entre elas.

### Roteamento Dinâmico:
Se você precisa de rotas dinâmicas, o Vue Router pode ser utilizado para criar rotas com parâmetros e rotas aninhadas.

### Navegação Programática:
O Vue Router facilita a navegação programática entre as rotas, permitindo que você navegue entre as rotas de forma imperativa.

### Exemplos Práticos de Uso do Vue Router:
Exemplo 1: Rotas Simples:
`
<!-- main.js -->
import { createRouter, createWebHistory } from 'vue-router';
import { createApp } from 'vue';
import App from './App.vue';

const router = createRouter({
  history: createWebHistory(),
  routes: [
    {
      path: '/',
      component: Home,
    },
    {
      path: '/about',
      component: About,
    },
  ],
});

createApp(App).use(router).mount('#app');
`
`
<!-- App.vue -->
<template>
  <div>
    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>
    <router-view></router-view>
  </div>
</template>
`

Neste exemplo, criamos um roteador simples com duas rotas: Home e About. O componente App utiliza o router-link para navegar entre as rotas e o router-view para renderizar o componente correspondente à rota atual.

Exemplo 2: Rotas Dinâmicas:
`
<!-- main.js -->
import { createRouter, createWebHistory } from 'vue-router';
import { createApp } from 'vue';
import App from './App.vue';

const router = createRouter({
  history: createWebHistory(),
  routes: [
    {
      path: '/user/:id',
      component: User,
    },
  ],
});

createApp(App).use(router).mount('#app');
`
`
<!-- App.vue -->
<template>
  <div>
    <router-link to="/user/1">User 1</router-link>
    <router-link to="/user/2">User 2</router-link>
    <router-view></router-view>
  </div>
</template>
`

Neste exemplo, criamos uma rota dinâmica com um parâmetro id. O componente App utiliza o router-link para navegar entre as rotas e o router-view para renderizar o componente correspondente à rota atual.

Exemplo 3: Rotas Aninhadas:
`
<!-- main.js -->
import { createRouter, createWebHistory } from 'vue-router';
import { createApp } from 'vue';
import App from './App.vue';

const router = createRouter({
  history: createWebHistory(),
  routes: [
    {
      path: '/user/:id',
      component: User,
      children: [
        {
          path: 'profile',
          component: Profile,
        },
        {
          path: 'settings',
          component: Settings,
        },
      ],
    },
  ],
});

createApp(App).use(router).mount('#app');
`
`
<!-- App.vue -->
<template>
  <div>
    <router-link to="/user/1/profile">User 1 Profile</router-link>
    <router-link to="/user/1/settings">User 1 Settings</router-link>
    <router-view></router-view>
  </div>
</template>
`

Neste exemplo, criamos rotas aninhadas para o usuário com id 1. O componente App utiliza o router-link para navegar entre as rotas e o router-view para renderizar o componente correspondente à rota atual.

Exemplo 4: Navegação Programática:
`
<!-- main.js -->
import { createRouter, createWebHistory } from 'vue-router';
import { createApp } from 'vue';
import App from './App.vue';

const router = createRouter({
  history: createWebHistory(),
  routes: [
    {
      path: '/user/:id',
      component: User,
    },
  ],
});

createApp(App).use(router).mount('#app');
`
`
<!-- App.vue -->
<template>
  <div>
    <router-link to="/user/1">User 1</router-link>
    <router-link to="/user/2">User 2</router-link>
    <router-view></router-view>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router';

const router = useRouter();

const navigateToUser = (id) => {
  router.push(`/user/${id}`);
};
</script>
`

Neste exemplo, criamos um roteador simples com uma rota dinâmica. O componente App utiliza o router-link para navegar entre as rotas e o router-view para renderizar o componente correspondente à rota atual. O componente também utiliza o useRouter para navegar programaticamente para uma rota específica.
