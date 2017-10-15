<template>
    <div>
        <!-- DEPARTMENTS -->
         <section id="departments" >
            <div class="container section">
                <div class="row">
                    <h1 class="centered-hor section-head">
                        Departments
                    </h1>
                </div>

                <!-- Determine which component to load based on the screen size -->
                <span v-for="d_row in departments"> <!-- ITERATOR -->
             
                    <div class="row centered-hor">
                        <div class="c4 columns centered-hor">

                            <!-- First of the first row -->
                            <div class="top-margin">        
                                <!-- pictures need to be changed -->
                                <img src="../assets/lnr-thumbs-up.svg" style="height: 80px;" class="value-img" />
                                <h5>{{d_row.instances[0].title}}</h5>
                                <h6>{{d_row.instances[0].text}}</h6>
                                <a @click="selectDepartment(d_row, 0)">{{MORE_ANCHOR}}</a>
                            </div>
                            
                            <!-- The shifted ones -->
                            <span v-if="!isSelectorEmpty(d_row)">
                                <div class="top-margin">        
                                    <img src="../assets/lnr-thumbs-up.svg" style="height: 80px;" class="value-img" />
                                    <h5>{{d_row.instances[1].title}}</h5>
                                    <h6>{{d_row.instances[1].text}}</h6>
                                    <a @click="selectDepartment(d_row, 1)">{{MORE_ANCHOR}}</a>
                                </div>
                                
                                <div class="top-margin">        
                                    <img src="../assets/lnr-thumbs-up.svg" style="height: 80px;" class="value-img" />
                                    <h5>{{d_row.instances[2].title}}</h5>
                                    <h6>{{d_row.instances[2].text}}</h6>
                                    <a @click="selectDepartment(d_row, 2)">{{MORE_ANCHOR}}</a>
                                </div>
                            </span>
                        </div>

                        <!-- The selected one -->
                        <div id="departmentDetailsPane"
                                class="c6 off-c2 columns centered-hor top-margin"  
                                v-if="!isSelectorEmpty(d_row)">
                            <div>
                                <h3><i class="fa fa-angle-left fa-1" 
                                        @click="clearSelection()"></i>
                                        &#160;
                                        &#160; 
                                        {{d_row.selected.title}}
                                        &#160;
                                        &#160; 
                                        &#160; 
                                        </h3>
                            </div>
            
                            <div class="top-margin-sm">
                                <h5>{{d_row.selected.department_head}} ~ $ </h5>
                                <h6>{{d_row.selected.text_full}}</h6>
                                <ul>
                                    <li></li>
                                </ul>
                            </div>
                        </div>

                        <!-- The normal rest (none selected) -->
                        <div class="c4 columns centered-hor" v-if="isSelectorEmpty(d_row)">
                            <div class="top-margin">      
                                <!-- pictures need to be changed -->
                                <img src="../assets/lnr-thumbs-up.svg" style="height: 80px;" class="value-img" />
                                <h5>{{d_row.instances[1].title}}</h5>
                                <h6>{{d_row.instances[1].text}}</h6>
                                <a @click="selectDepartment(d_row, 1)">{{MORE_ANCHOR}}</a>
                            </div>
                        </div>
                        <div class="c4 columns centered-hor" v-if="isSelectorEmpty(d_row)">
                            <div class="top-margin">      
                                <!-- pictures need to be changed -->
                                <img src="../assets/lnr-thumbs-up.svg" style="height: 80px;" class="value-img" />
                                <h5>{{d_row.instances[2].title}}</h5>
                                <h6>{{d_row.instances[2].text}}</h6>
                                <a @click="selectDepartment(d_row, 2)">{{MORE_ANCHOR}}</a>
                            </div>
                        </div>
                        
                    </div>

                </span> <!-- END OF ITERATOR -->
            </div>
        </section>
    </div>
</template>

<script>

    // TOOD: add dynamic loading of the departments
    // TODO: change department pictures
    // TODO: add animations 

    export default {
        data() {
          return {
            title: "TEAM",
            MORE_ANCHOR: "more...",
            anchors: [
                
            ],
            departments: [
                {
                   
                    instances:[
                        {
                            title: 'Administration',
                            text:'Feed other students, share drinks and have fun'
                        },
                        {
                            title: 'Internal & External',
                            text:'Meet other students, share drinks and have fun'
                        },
                        {
                            title: 'Internal & External',
                            text:'Meet other students, share drinks and have fun'
                        }
                    ],
                    selected: {},
                },
                {
                    instances:[
                        {
                            title: 'Infrastructure',
                            text: 'Infrastructure Team @ Proxy is there to build services that help organizing fun events, ...',
                            text_full: 'Infrastructure Team @ Proxy is there to build services that help organizing fun events, create new cool online facilities and experiment!',
                            department_head: 'Dmitrii Orlov',
                            tasks: [
                                'Maintain Proxy website',
                                'Build experimental services',
                                'Fixing your routers'
                            ],
                            contacts: {
                                email: 'm.orlov@student.fontys.nl',
                                facebook: 'https://www.facebook.com/dmitry.orlov.104'
                            }

                        },
                        {
                            title: 'Internal & External',
                            text:'Meet other students, share drinks and have fun'
                        },
                        {
                            title: 'Teaching',
                            text:'Meet other students, share drinks and have fun'
                        }
                    ],
                    selected: {},
                }
            ],
          }
        },
        // computed: {
        //     isSelectorActive: function(d_row) {
        //         return d_row.selected;
        //     }
        // },
        methods: {
            selectDepartment: function(row, index) {
                console.log('selecting');
                for(let i in this.departments){this.departments[i].selected = {};}
                row.selected = row.instances[index];
            },
            clearSelection: function() {
                for(let i in this.departments){this.departments[i].selected = {};}
            },
            isSelectorEmpty: function(row){
                return Object.keys(row.selected).length === 0 && row.selected.constructor === Object
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

        }
    }
</script>