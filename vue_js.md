Для создания переменной необходимо создать в <script> export default { data() return{ {var_name: value,}}} - Чтобы была возможность обращать к переменным в data, в коде необходимо добавлять this.nameVar

Для обработки события можно добавлять события по форме: @click и т.д.

Для создания своих функций необходимо указать methods: { userData() {} }  

Привязка данных происходит при помощи атрибута v-model="nameVar"

Чтобы создать цикл переборки массива необходимо: div v-for="(el, index) in array" : key="index"

Чтобы создать ветвление необходимо: div v-if="userVar" и div v-else-if="userVar" и div v-else="userVar"

Чтобы использовать компоненты Vue необходимо:
* import CompName from 'route'
* export default { componens: {CompName},}

Чтобы создавать Vue атрибуты необходимо:
* создать атрибут :atName="value"
* в дочернем компоненте необходимо добавить export default { props: {value:{type:, required:,},}

Для получения данных из API необходимо установить библиотеку axios "npm i axios"
