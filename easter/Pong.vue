<template>
<div ref="pongModal" class="modal inmodal" tabindex="-1" role="dialog" aria-hidden="true">
    <div class="modal-dialog modal-lg">
        <div class="modal-content animated flipInY">
            <div class="modal-header">
                <button type="button" class="close" data-dismiss="modal"><span aria-hidden="true">&times;</span><span
                            class="sr-only">Close</span></button>
                <h4 class="modal-title"><strong>Pong<span class="text-warning">+</span></strong></h4>
            </div>
            <div class="modal-body">
                    <div class="easter-container">
                        <canvas id="pong" width="600" height="500">
                            This browser can not run this game (canvas support missing).
                        </canvas>
                    </div>
            </div>
        </div>
    </div>
</div><!-- Termo de Uso -->
</template>

<script>
import Game from "../../plugins/pong/Game.js";

export default {

    data() {

        return {

            pongGame: null
        }
    },

    mounted() {

        Event.$on('showEaster', () => {
            
            $(this.$refs.pongModal).modal('show');

            if (!this.pongGame) {
                
                this.pongGame = new Game("pong");
    
                this.pongGame.number_of_players = 1;
                this.pongGame.difficulty = 5;
                this.pongGame.start();
            } else {

                this.pongGame.restart();
            }

        });
    }
}
</script>

<style scoped>
    canvas
    {
        margin: 0px auto;
    }
    .easter-container
    {
        text-align: center;
    }
</style>
