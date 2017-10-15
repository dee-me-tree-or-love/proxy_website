<template>
    <div>
    
        <!-- NAVBAR -->
        <app-nav :sublinks="anchors" :title="title"></app-nav>
        <!-- END OF NAVBAR -->

        <!-- WELCOME -->
        <!-- issue: pictures relaod only on hard cache clean -->
        <header id="fullscreenimage">
            <!--header contains the background picture in css-->
            <div id="welcome" class="container center-wrap" >
                <div class="centered-hor centered-ver" style="height:inherit;">
                    <!--content goes here-->
                    <div>
                        <h1 class="white-txt superfont">Our Team</h1>
                    </div>
                </div>
            </div>
        </header>
        <!-- END OF WELCOME -->


        <!-- DEPARTMENTS -->
        <dep-large v-if="isLargeEnough()"></dep-large>
        
        <!-- FOOTER -->
        <app-footer></app-footer>
    </div>
</template>

<script>

    // TOOD: add dynamic loading of the departments
    // TODO: change department pictures
    // TODO: add animations 

    import Nav from '../_shared/Navigation.vue'
    import Footer from '../_shared/Footer.vue'
    import DepLarge from './DepLarge.vue'

    export default {
        data() {
          return {
            title: "TEAM",
            anchors: [
                
            ],
          }
        },
        // computed: {
        //     isSelectorActive: function(d_row) {
        //         return d_row.selected;
        //     }
        // },
        methods: {
            isLargeEnough: function() {
                let width = (window.innerWidth > 0) ? window.innerWidth : screen.width;
                this.width = width;
                return this.width > 560;
            }
        },
        created(){

             function adjustHeader(){
                
                let wh = document.body.clientHeight;
                console.log(wh);
                let welcome = document.getElementById('welcome');
                // 1/2 of the screen size
                // welcome.style.height = Math.floor(wh/2) +'px';
                // fullscreen
                welcome.style.height = Math.floor(wh) +'px';
                console.log("resized");
            }
            document.addEventListener("DOMContentLoaded", function(event) {
                adjustHeader();
            });
            window.onresize = adjustHeader; 

        },
        components: {
            'app-nav': Nav,
            'app-footer': Footer,
            'dep-large': DepLarge,
        }
    }
</script>

<style scoped>
header{
    background: linear-gradient( rgba(255, 125, 125, 0.6), 
        rgba(75, 75, 75, 0.6), rgba(0, 0, 0, 0.6)), url(https://proxy-ict-api.herokuapp.com/img/team);
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    background-attachment: fixed;
}
</style>