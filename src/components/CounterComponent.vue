<template>
    <div class="counter-component">
        <div class="code">
            <pre>
                <code>
                // Local component state

                const state = reactive({ count: 0, counterDetails: { count: 0 }})

                let { count, counterDetails } = state

                setInterval(() => { count++; updateCount(counterDetails) }, 1000)

                const updateCount = counterObj => { counterObj.count++ }
                </code>
            </pre>
            <pre>
                <code>
                    // props

                    const { counterDetailsProp } = props

                    return { value: counterDetailsProp }
                </code>
            </pre>
        </div>
        <div class="output">
            <div class="local-state">
                <div class="scenario">
                    <div>{{ count }}</div>
                    <div>count</div>
                </div>
                <div class="scenario">
                    <div>{{ counterDetails.count }}</div>
                    <div>counterDetails.count</div>
                </div>
            </div>
            <div class="props">
                <div class="scenario">
                    <div>{{ countProp }}</div>
                    <div>countProp</div>
                </div>
                <div class="scenario">
                    <div>{{ counterDetailsProp.count }}</div>
                    <div>counterDetailsProp.count</div>
                </div>
                <div class="scenario">
                    <div>{{ value.count }}</div>
                    <div>value.count</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { reactive } from '@vue/reactivity'
import { watch } from '@vue/runtime-core'

export default {
    props: {
        countProp: {
            type: Number,
            required: true
        },
        counterDetailsProp: {
            type: Object,
            required: true
        }
    },
    setup(props) {
        const state = reactive({
            count: 0,
            counterDetails: {
                count: 0
            }
        })

        let { count } = state
        const counterDetails = state.counterDetails

        setInterval(() => {
            count++
            updateCount(counterDetails)
        }, 1000)

        const updateCount = counterObj => {
            counterObj.count++
        }

        // eslint-disable-next-line vue/no-setup-props-destructure
        const { counterDetailsProp } = props
        watch(counterDetailsProp, () => {
            console.log('prop counterDetailsProp changed. new value is ', counterDetailsProp.count)
        })
        
        return {
            count,
            counterDetails,
            value: counterDetailsProp
        }
    }
}
</script>

<style scoped>
.counter-component {
    width: 100vw;
    height: 100vh;
    display: flex;
}
.counter-component .code {
    width: 50%;
    height: 100vh;
}
.counter-component .code pre {
    height: 50%;
    border: solid 1px gray;
    border-bottom: solid 2px red;
    margin: 0;
    display: flex;
    align-items: center;
}
.counter-component .output {
    width: 50%;
    height: 100vh;
}
.counter-component .output .local-state {
    display: flex;
    height: 50%;
}
.counter-component .output .props {
    display: flex;
    height: 50%;
}
.counter-component .output .local-state .scenario {
    width: 50%;
    border: solid 1px gray;
    border-bottom: solid 2px red;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}
.counter-component .output .props .scenario {
    width: 33%;
    border: solid 1px gray;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}
</style>