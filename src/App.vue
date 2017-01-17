<template>
<div id="app">
    <h1>Vue Grid Layout</h1>
    <!--<pre>{{ layout | json }}</pre>-->
    <div>
        <div class="layoutJSON">
            Displayed as <code>[x, y, w, h]</code>:
            <div class="columns">
                <div class="layoutItem" v-for="item in layout">
                    <b>{{item.i}}</b>: [{{item.x}}, {{item.y}}, {{item.w}}, {{item.h}}]
                </div>
            </div>
        </div>
    </div>
    <div id="content">
        <button @click="decreaseWidth">Decrease Width</button>
        <button @click="increaseWidth">Increase Width</button>
        <button @click="addItem">Add an item</button>
        <br/>
        <grid-layout :layout="layout" :col-num="12" :row-height="30" :is-draggable="true" :is-resizable="true"
            :vertical-compact="true" :use-css-transforms="true">
            <grid-item v-for="item in layout" :x="item.x" :y="item.y" :w="item.w" :h="item.h" :min-w="2" :min-h="2"
                :i="item.i" @resized="resized">
                <test-element :text="item.i"></test-element>
                </grid-item>
                </grid-layout>
    </div>
</div>

</template>

<script>
import GridItem from './GridItem.vue';
import GridLayout from './GridLayout.vue';
//import ResponsiveGridLayout from './ResponsiveGridLayout.vue';
import TestElement from './TestElement.vue';

var testLayout = [{
    "x": 0,
    "y": 0,
    "w": 2,
    "h": 2,
    "i": "0"
}, ];

export default {
    name: 'app',
    components: {
        //ResponsiveGridLayout,
        GridLayout,
        GridItem,
        TestElement,
    },
    data() {
        return {
            layout: JSON.parse(JSON.stringify(testLayout)),
            colNum: 0,
            index: 0
        }
    },
    mounted: function() {
        this.index = this.layout.length;
    },
    methods: {
        resized: function(msg) {
            console.log(msg);
        },
        increaseWidth: function(item) {
            var width = document.getElementById("content").offsetWidth;
            width += 20;
            document.getElementById("content").style.width = width + "px";
        },
        decreaseWidth: function(item) {

            var width = document.getElementById("content").offsetWidth;
            width -= 20;
            document.getElementById("content").style.width = width + "px";
        },
        removeItem: function(item) {
            //console.log("### REMOVE " + item.i);
            this.layout.splice(this.layout.indexOf(item), 1);
        },
        addItem: function() {
            var self = this;
            //console.log("### LENGTH: " + this.layout.length);
            var item = {
                "x": 0,
                "y": 0,
                "w": 2,
                "h": 2,
                "i": this.index + "",
                whatever: "bbb"
            };
            this.index++;
            this.layout.push(item);
        }
    },
}

</script>

<style>
/*    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }

    h1, h2 {
        font-weight: normal;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }*/

</style>
