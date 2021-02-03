<template>
    <div id="app">
        <!-- learn the basic building blocks of HTML. 
        Using divs for everything is a common thing I see, but it's visually confusing and non-semantic -->
        <header>
            <h2>I am always present on the page</h2>
        </header>

        <component
            :is="componentDef"
            v-bind="currentNode"
            @select="down"
            @back="up"
        ></component>
    </div>
</template>


<script>
import welcomeData from "./welcome.json";

import Topic from "./components/Topic";
import Subtopic from "./components/Subtopic";
import Slideshow from "./components/Slideshow";

export default {
    components: {
        Topic,
        Subtopic,
        Slideshow,
    },
    data() {
        return {
            breadcrumbs: [],
        };
    },
    computed: {
        depth() {
            return this.breadcrumbs.length;
        },
        currentNode() {
            return this.breadcrumbs.reduce((node, i) => {
                return node.children[i];
            }, welcomeData);
        },
        kids() {
            return this.currentNode.children;
        },
        componentDef() {
            switch (this.depth) {
                case 0:
                    return Topic;
                case 1:
                    return Subtopic;
                default:
                    return Slideshow;
            }
        },
    },
    methods: {
        // drill down to next layer
        down(childIndex) {
            this.breadcrumbs.push(childIndex);
        },
        // back up to previous layer
        up() {
            this.breadcrumbs.pop();
        },
    },
};
</script>
