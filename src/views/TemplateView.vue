<script setup>
import { ref, onMounted, computed, reactive } from 'vue'

// reactive state
const count = ref(12);
const firstName = ref('');
const lastName = ref('');
const classCheck = ref(false);
const showHello = ref(false);
const inlineSyleCheck = ref('color:red');
const reactiveClass = reactive({
    textDecorationine: 'overline',
    backgroundColor: 'yellow',
    color: 'blue',
})
const fontSize = ref(count);
const topics = reactive([
    { topic: 'Examples', path: '#Examples' },
    { topic: 'Template Syntax', path: '#TemplateSyntax' },
    { topic: 'Reactivity Fundamentals​', path: '#ReactivityFundamentals​' },
    { topic: 'Computed Properties​', path: '#ComputedProperties' },
    { topic: 'Class and Style Bindings', path: '#ClassandStyleBindings' },
    { topic: 'Conditional Rendering', path: '#ConditionalRendering' },
    { topic: 'List Rendering', path: '#ListRendering' },
    { topic: 'Reactivity Fundamentals', path: '#TemplateSyntax' },
])

// functions that mutate state and trigger updates
function increment() {
    return count.value++;
}

const helloDisplay = () => {
    showHello.value = !showHello.value;
}

function changeFirstName(event) {
    firstName.value = event.target.value
}
function changeLastName(event) {
    lastName.value = event.target.value
}

let FullName = computed(() => {
    console.log("computed from full name var");
    if (firstName.value.length > 3) {
        inlineSyleCheck.value = 'color:blue'
    }
    else {
        inlineSyleCheck.value = 'color:red'
    }
    return firstName.value + " " + lastName.value;
})
let countComp = computed(() => {
    let c = count.value;
    if (c >= 3) {
        classCheck.value = true;
    }
    console.log("computed from count var");
    return "your computed count is " + c;
})

// lifecycle hooks
onMounted(() => {
    console.log(`The initial count is ${count.value}.`)
    console.log("one line added");
})

</script>

<template>
    <div>

    </div>
    <div class="row mt-5">
        <div id="list-example" class="list-group col-md-4">
            <a class="list-group-item list-group-item-action" v-for="(topic, index) in topics" v-bind:href="topic.path"
                v-bind:key="index">{{ topic.topic
                }}</a>
        </div>
        <div data-bs-spy="scroll" data-bs-target="#list-example" data-bs-offset="0"
            class="scrollspy-example col-md-8 position-static" tabindex="0">
            <h4 id="Examples">Examples of all the topic in one</h4>
            <p>
            <div class="mt-3 h4">>> Counts : {{ count }} <span
                    :class="[classCheck ? 'text-info' : 'text-decoration-line-through']">{{ countComp }}</span></div>
            <button v-on:click="increment" class="btn btn-warning mt-3">Count increment</button>
            <h3 class="mt-3" :style="inlineSyleCheck">{{ FullName }}</h3>
            <div class="row mt-2">
                <div class=" col-6 mt-2">
                    <input placeholder="First Name" @input="changeFirstName" class="form-control" />
                </div>
                <div class="col-6 mt-2">
                    <input placeholder="Last Name" @input="changeLastName" class="form-control" />
                </div>
            </div>

            <div class="col-4">
                <h2 class="mt-3" :style="reactiveClass" v-show="showHello">{{ count }}</h2>
                <h2 class="mt-3" v-if="showHello" :style="{ 'fontSize': fontSize + 'px' }">v-if entred</h2>
                <h2 class="mt-3" v-else="showHello" :style="{ 'fontSize': fontSize + 'px' }">v-else entred</h2>

                <button :style="[showHello ? 'reactiveClass' : '']" class="btn btn-success mt-3" @click="helloDisplay">Show
                    Count</button>
            </div>
            </p>
            <h4 id="TemplateSyntax">Template Syntax</h4>
            <p>
            <h5 class="mt-3">overview of the session</h5>
            <ul>
                <li>Text Interpolation is covered. we can write the data with the "mustache" to bind the vue variable with
                    the html the syntaxt is {{ }} in double curly braces</li>
                <li>raw html with the help of vue directives like v-html we can bind the html with the template using js.
                </li>
            </ul>
            </p>
            <h4 id="ReactivityFundamentals">Reactivity Fundamentals</h4>
            <p>
            <ul>
                <li>Reactivity is the ability of the variable to update when it's value or any other dependency of that
                    variable is changed</li>
                <li>The changes is reflected to the UI when the values is changed with reloading that template tag in the
                    component</li>
                <li>It only works for object types (objects, arrays, and collection types such as Map and Set). It cannot
                    hold primitive types such as string, number or boolean.</li>
            </ul>
            </p>
            <h4 id="ComputedProperties">Computed Properties</h4>
            <p>
            <ul>
                <li>In Vue. js, computed properties enable you to create a property that can be used to modify, manipulate,
                    and display data within your components in a readable and efficient manner</li>
                <li>A computed property is used to declaratively describe a value that depends on other values. </li>
            </ul>
            </p>
            <h4 id="ClassandStyleBindings">Class and Style Bindings</h4>
            <p>
            <ul>
                <li>
                    we can bind the html css with the vue dynamically using the v-bind directives
                </li>
                <li>A common need for data binding is manipulating an element's class list and inline styles. Since class
                    and style are both attributes, we can use v-bind to assign them a string value dynamically, much like
                    with other attributes. However, trying to generate those values using string concatenation can be
                    annoying and error-prone. For this reason, Vue provides special enhancements when v-bind is used with
                    class and style. In addition to strings, the expressions can also evaluate to objects or arrays.</li>
            </ul>
            </p>
            <h4 id="ConditionalRendering">Conditional Rendering</h4>
            <p>
            <ul>
                <li>
                    for the conditional check what is to be done. In vue js we can do the if else-if and else using the
                    directive.
                    <ul>
                        <li>v-if</li>
                        <li>v-else-if</li>
                        <li>v-else</li>
                        <li>v-show</li>
                    </ul>
                </li>
                <li>
                    v-if: It works similarly as if work work. it will check the directive expression and return if the
                    truthy value is return.
                    we can write the v-if in the template tag. This directive will remove the block from the dom if return
                    falsy.
                </li>
                <li>v-else: It also work same as the else block</li>
                <li>v-else-if: It will do work like the else if block does.</li>
                <li>v-show: This is replica of the v-if but the change is this will not remove from the dom instead it will
                    togglw with the css display property</li>
            </ul>
            </p>
            <h4 id="ListRendering">List Rendering</h4>
            <p>
                <li>
                    v-for is used to display the items in tha array. the syntax for the v-for is v-for="item in items" the
                    items are the source array and item is the alias for the array elements.
                </li>
                <li>v-for can to itrate throught the properties of the objects. it will return the result of the object.keys
                    (i.e array of string)</li>
                <li>we can use the v-foe with the template</li>
                <li>If we use the v-if and v-for on the same node/element then the v-if has the highre priority then v-for
                </li>
            </p>

            <h4 id="EventHandling">Event Handling</h4>
            <p></p>

        </div>
    </div>
</template>
