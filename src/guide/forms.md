---
title: Input Bindings em Formulários
type: guide
order: 10
---

## Uso Básico

Você pode usar a diretiva `v-model` para criar two-way data bindings em elementos input e textarea de formulários. Ele automaticamente busca a maneira correta de atualizar o elemento com base no tipo de entrada. Embora um pouco mágico, `v-model` é essencialmente syntax sugar para atualização de dados com eventos de entrada do usuário, além de cuidados especiais para alguns casos do edge.

<p class="tip">`v-model` não se importa com o valor inicial fornecido para um input ou um textarea. Ele sempre vai tratar os dados de instância do Vue como a fonte verdadeira.</p>

### Texto

``` html
<input v-model="message" placeholder="Me edite">
<p>A mensagem é: {{ message }}</p>
```

{% raw %}
<div id="example-1" class="demo">
  <input v-model="message" placeholder="Me edite">
  <p>A mensagem é: {{ message }}</p>
</div>
<script>
new Vue({
  el: '#example-1',
  data: {
    message: ''
  }
})
</script>
{% endraw %}

### Texto com múltiplas linhas

``` html
<span>A mensagem com múltiplas linhas é:</span>
<p style="white-space: pre">{{ message }}</p>
<br>
<textarea v-model="message" placeholder="Adicione múltiplas linhas"></textarea>
```

{% raw %}
<div id="example-textarea" class="demo">
  <span>A mensagem com múltiplas linhas é:</span>
  <p style="white-space: pre">{{ message }}</p><br>
  <textarea v-model="message" placeholder="Adicione múltiplas linhas"></textarea>
</div>
<script>
new Vue({
  el: '#example-textarea',
  data: {
    message: ''
  }
})
</script>
{% endraw %}

<p class="tip">Interpolação em textareas (<code>&lt;textarea&gt;{{text}}&lt;/textarea&gt;</code>) não funciona. Em vez disso use <code>v-model</code>.</p>

### Checkbox

Checkbox único, valor boleano:

``` html
<input type="checkbox" id="checkbox" v-model="checked">
<label for="checkbox">{{ checked }}</label>
```
{% raw %}
<div id="example-2" class="demo">
  <input type="checkbox" id="checkbox" v-model="checked">
  <label for="checkbox">{{ checked }}</label>
</div>
<script>
new Vue({
  el: '#example-2',
  data: {
    checked: false
  }
})
</script>
{% endraw %}

Múltiplos checkboxes, associados ao mesmo Array:

``` html
<input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
<label for="jack">Jack</label>
<input type="checkbox" id="john" value="John" v-model="checkedNames">
<label for="john">John</label>
<input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
<label for="mike">Mike</label>
<br>
<span>Nomes assinalados: {{ checkedNames }}</span>
```

``` js
new Vue({
  el: '...',
  data: {
    checkedNames: []
  }
})
```

{% raw %}
<div id="example-3" class="demo">
  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
  <label for="jack">Jack</label>
  <input type="checkbox" id="john" value="John" v-model="checkedNames">
  <label for="john">John</label>
  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
  <label for="mike">Mike</label>
  <br>
  <span>Nomes assinalados: {{ checkedNames }}</span>
</div>
<script>
new Vue({
  el: '#example-3',
  data: {
    checkedNames: []
  }
})
</script>
{% endraw %}

### Radio


``` html
<input type="radio" id="one" value="Um" v-model="picked">
<label for="one">Um</label>
<br>
<input type="radio" id="two" value="Dois" v-model="picked">
<label for="two">Dois</label>
<br>
<span>Escolhido: {{ picked }}</span>
```
{% raw %}
<div id="example-4" class="demo">
  <input type="radio" id="one" value="Um" v-model="picked">
  <label for="one">Um</label>
  <br>
  <input type="radio" id="two" value="Dois" v-model="picked">
  <label for="two">Dois</label>
  <br>
  <span>Escolhido: {{ picked }}</span>
</div>
<script>
new Vue({
  el: '#example-4',
  data: {
    picked: ''
  }
})
</script>
{% endraw %}

### Select

Select único:

``` html
<select v-model="selected">
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
<span>Selecionado: {{ selected }}</span>
```
{% raw %}
<div id="example-5" class="demo">
  <select v-model="selected">
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <span>Selecionado: {{ selected }}</span>
</div>
<script>
new Vue({
  el: '#example-5',
  data: {
    selected: null
  }
})
</script>
{% endraw %}

Select múltiplo (ligados a um array):

``` html
<select v-model="selected" multiple>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
<br>
<span>Selecionados: {{ selected }}</span>
```
{% raw %}
<div id="example-6" class="demo">
  <select v-model="selected" multiple style="width: 50px">
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <br>
  <span>Selecionados: {{ selected }}</span>
</div>
<script>
new Vue({
  el: '#example-6',
  data: {
    selected: []
  }
})
</script>
{% endraw %}

Options dinamicamente renderizados com `v-for`:

``` html
<select v-model="selected">
  <option v-for="option in options" v-bind:value="option.value">
    {{ option.text }}
  </option>
</select>
<span>Selecionado: {{ selected }}</span>
```
``` js
new Vue({
  el: '...',
  data: {
    selected: 'A',
    options: [
      { text: 'Um', value: 'A' },
      { text: 'Dois', value: 'B' },
      { text: 'Três', value: 'C' }
    ]
  }
})
```
{% raw %}
<div id="example-7" class="demo">
  <select v-model="selected">
    <option v-for="option in options" v-bind:value="option.value">
      {{ option.text }}
    </option>
  </select>
  <span>Selecionado: {{ selected }}</span>
</div>
<script>
new Vue({
  el: '#example-7',
  data: {
    selected: 'A',
    options: [
      { text: 'Um', value: 'A' },
      { text: 'Dois', value: 'B' },
      { text: 'Três', value: 'C' }
    ]
  }
})
</script>
{% endraw %}

## Value Bindings

Para radio, checkbox e select options, os binding values do `v-model` são normalmente strings estáticas (ou boleano para checkbox):


``` html
<!-- `picked` é uma string "a" quando assinalado -->
<input type="radio" v-model="picked" value="a">

<!-- `toggle` é verdadeiro ou falso -->
<input type="checkbox" v-model="toggle">

<!-- `selected` é uma string "abc" quando assinalado -->
<select v-model="selected">
  <option value="abc">ABC</option>
</select>
```

Mas às vezes podemos querer vincular o valor de uma propriedade dinâmica na instância do Vue. Podemos usar 'v-bind' para alcançar esse objectivo. Além disso, usando 'v-bind' nos permite vincular o valor de inputs para valores de sequências non-string.

### Checkbox

``` html
<input
  type="checkbox"
  v-model="toggle"
  v-bind:true-value="a"
  v-bind:false-value="b">
```

``` js
// quando está assinalado:
vm.toggle === vm.a
// quando não está assinalado:
vm.toggle === vm.b
```

### Radio

``` html
<input type="radio" v-model="pick" v-bind:value="a">
```

``` js
// quando está assinalado:
vm.pick === vm.a
```

### Select Options

``` html
<select v-model="selected">
  <!-- Objeto literal inline -->
  <option v-bind:value="{ number: 123 }">123</option>
</select>
```

``` js
// quando está assinalado:
typeof vm.selected // -> 'object'
vm.selected.number // -> 123
```

## Modificadores

### `.lazy`


Por padrão, `v-model` sincroniza o input com os dados após cada evento de `input`. Adicionando o modificador `lazy` a sincronização ocorrerá somente após o evento `change`:

``` html
<!-- sincronizado depois do "change" ao invés de "input" -->
<input v-model.lazy="msg" >
```

### `.number`

Se você quer que a entrada do usuário seja tipificada como um número, isso pode ser feito adicionando o modificador `number` ao `v-model` do input:

``` html
<input v-model.number="age" type="number">
```

Isso é bastante útil, porque mesmo com `type="number"`, o valor HTML retornado é sempre uma string.

### `.trim`

Se você que que a entrada do usuário seja automaticamente isenta de espaços no início e no fim, você pode adicionar o modificador `trim` ao `v-model` do input:


```html
<input v-model.trim="msg">
```
