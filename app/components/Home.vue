<template>
    <Page class="page">
        <ActionBar class="action-bar">
            <Label class="action-bar-title" text="Shakespeare Insult Machine 🥀"></Label>
        </ActionBar>

        <GridLayout rows="*, 100">
            <Label row="0" class="insult" textWrap="true" horizontalAlignment="center" verticalAlignment="center">
                <FormattedString>
                    <Span :text="insult"/>
                </FormattedString>
            </Label>
                <Button row="1" class="action"  @tap="generateInsult" text="Wilt thou insult me!" />
        </GridLayout>
    </Page>
</template>

<script>
import insults from '../data/sik';
import { Random } from "random-js";

const random = new Random();

    export default {
        data() {
            return {
                randomNumbers: [0,0,0],
            }
        },
        computed: {
            insult() {
                return `Thou ${insults.verb[this.randomNumbers[0]]} ${insults.adjective[this.randomNumbers[1]]} ${insults.noun[this.randomNumbers[2]]}!`;
            }
        },
        created() {
            this.generateInsult();
        },
        methods: {
            generateInsult() {
                const selection = {
                    verb: random.integer(0, insults.verb.length-1),
                    adjective: random.integer(0, insults.adjective.length-1),
                    noun: random.integer(0, insults.noun.length-1),
                    };
                this.randomNumbers = [selection.verb, selection.adjective, selection.noun];
            }
        }
    };
</script>

<style scoped lang="scss">
    // Start custom common variables
    @import '../app-variables';
    // End custom common variables

    // Custom styles
    .page {
        color: #252024;
        background: rgb(110,69,85);
        background: linear-gradient(0deg, rgba(110,69,85,1) 0%, rgba(210,130,166,1) 35%, rgba(232,180,188,1) 100%);
    }

    .action-bar {
        background-color: #F5E3E0;
        color: #3A3238;
    }

    .insult {
        font-size: 60;
        text-align: center;
        font-style: italic;
        background: transparent;
        font-weight: 700;
    }


    .action {
        background-color: #3A3238;
        color: #F5E3E0;
        font-size: 18;
        font-weight: 700;
    }


</style>
