<template>
    <div class="fader-box" :data-cue="cue" v-bind:style="{
                'background-color':backgroundColor,
				'color': textColor
			}">
        <div class="info-box-content">
            <span class="info-box-icon" :class="color"><i class="fa" :class="icon"></i></span>
            <span class="info-box-text">{{type}}</span>
            <span class="info-box-number">{{name}}</span>
        </div>
        <input type="range" orient="vertical" min="0" :max="cue.length - 1" value="0" @change="changeCue" ref="fader" v-model="currentCueIndex" />
    </div>
</template>


<script>
    import {bus} from './bus';
    module.exports = {
        props: {
            'cue' : {
                type: Array,
                required: true
            },
            'color' : {
                default: "bg-blue"
            },
            'icon' : {
                default: "fa-lightbulb-o"
            },
            'name' : {
                required: true
            },
            'type' : {
                default: "Presets"
            },
            'backgroundColor' : {
                type: String,
                default: '#fff'
            },
            'textColor' : {
                default: '#333'
            }
        },
        data: function() {
            return {
                'fading' : false,
                currentCueIndex : this.updatedActiveCues()
            }
        },
        methods: {
            changeCue: function(){
                let cue_index = this.currentCueIndex;
                let that = this;

                this.$props.cue.forEach((cue,loop_index) => {
                    cue_index = parseInt(cue_index);
                    if(loop_index === cue_index)
                        that.setCue(cue);
                    else
                        that.relCue(cue);
                });
            },
            updatedActiveCues: function(){
                console.log('updating cuelist');
                let that = this;
                this.$root.activeCuelists.forEach(function(each) {
                    that.$props.cue.forEach(function(cue,cue_index){
                        if(cue === each.id){
                            return cue_index;
                        }
                    });
                });
                return 0;
            },
            setCue: function(cue){
                this.$root.sendCommand('cuelistGo ' + cue);
            },
            relCue: function(cue){
                this.$root.sendCommand('cuelistRelease ' + cue);
            },
        },
    }
</script>

<style>
    input[type=range][orient=vertical]
    {
        writing-mode: bt-lr; /* IE */
        -webkit-appearance: slider-vertical; /* WebKit */
    }
    .fader-box .info-box-content {
        width: 100%;
        margin: 0;
        text-align: center;
    }

    .fader-box .info-box-content .info-box-icon {
        display: inline-block;
        float: none;
    }

    .fader-box input {
        margin: 0 auto;
        height: calc(100% - 145px);
    }

    .fader-box {
        text-align: center;
        height: 100%;
    }

    input[type=range] {
        -webkit-appearance: none;
        margin: 0 auto;
        width: 20px;
    }
    input[type=range]:focus {
        outline: none;
    }
    input[type=range]::-webkit-slider-runnable-track {
        width: 100%;
        height: 50px;
        cursor: pointer;
        animate: 1s ease all;
        box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
        background: #0073b7;
        border-radius: 1.3px;
        border: 0px solid #010101;
        transition: 1s ease all;
    }
    input[type=range]::-webkit-slider-thumb {
        box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
        border: 20px solid #000000;
        height: 100px;
        width: 50px;
        border-radius: 3px;
        background: #ffffff;
        cursor: pointer;
        -webkit-appearance: none;
        margin: 0px -10px 0px -10px;
    }
</style>