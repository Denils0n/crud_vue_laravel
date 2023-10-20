<script setup>
import { ref } from 'vue';

const DIST = 30

class P {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }

    toString() {
        return this.x + ',' + this.y
    }
}

class Node {
    constructor(p, parent) {
        this.p = p;
        this.parent = parent;
        this.ch = false
    }
}


const checkboxes = ref([])

const getStyle = (node) => {
    const [x, y] = (""+node.p).split(',')
    return `
        top: ${y*DIST}px;
        left: ${x*DIST}px;
    `
}

const create = (p, parent) => {
    if (checkboxes.value.some(x => ""+x.p == ""+p)) {
        return
    }
    console.log({p})
    checkboxes.value.push(new Node(p, parent))
}

const handleClick = (node) => {
    node.ch = !node.ch
    if (!node.ch) {
        // remove
        return
    }
    createNeighbours(node)

}

const createNeighbours = (node) => {
    const [x, y] = (""+node.p).split(',')
    console.log('neighbours', x, y)
    create(new P(+x + 1, +y), node.p)
    create(new P(+x - 1, +y), node.p)
    create(new P(+x, +y + 1), node.p)
    create(new P(+x, +y - 1), node.p)
}

create(new P(0, 0))

</script>

<template>
    <div class="flex justify-center min-h-screen align-center">
        <div class="absolute" v-for="node in checkboxes" :style="getStyle(node)">
            <input type="checkbox" @click="handleClick(node)" :checked="node.ch">
        </div>
    </div>
</template>
