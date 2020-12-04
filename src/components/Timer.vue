<template>
    <section class="timer">
        <div class="row justify-content-center">
            <div class="col-12">
                <h3>Timer</h3>
            </div>
            <div class="col-4">
                <div class="row text-center">
                    <div class="col-12">
                        <p>Elapsed time: {{progress}}</p>
                        <div class="progress">
                            <div class="progress-bar progress-bar-striped progress-bar-animated" role="progressbar" :aria-valuenow="progress" aria-valuemin="0" aria-valuemax="100" :style="progressStyle">{{fillProgress}} %</div>
                        </div>
                    </div>
                    <div class="col-12 text-center">
                        <h3>{{elapsedTime}}</h3>
                    </div>
                    <div class="form-group col-12">
                        <input v-model="elapsedTime" @change="startTimer()" min="0" max="100" type="range" class="custom-range" id="elapsed">
                    </div>
                    <button type="submit" @click="reset()" class="btn btn-purple mr-auto ml-auto">Reset</button>
                </div>
            </div>
        </div>
        
    </section>
</template>

<script>
export default {
    name: "Timer",
    data() {
        return {
            elapsedTime: 0,
            progress: 0,
            progressStyle: "width: 0",
            fillProgress: 0
        }
    },
    methods: {
        reset() {
            this.elapsedTime = 0
            this.progress = 0
            this.progressStyle = "width: 0"
        },
        startTimer() {
            setTimeout(this.fillProgressBar, 1)
        },
        fillProgressBar() {
            if (this.progress != this.elapsedTime) {
                this.progress++
                this.fillProgress = Math.round((this.progress*100) / this.elapsedTime)
                this.progressStyle = `width: ${this.fillProgress}%`
                setTimeout(this.fillProgressBar, 1000)
            } else {
                this.currentTime = null;
            }
        }
    }
}
</script>

<style scoped>
.btn-purple {
    color: #fff;
    background-color: #6542f4;
    border-color: #6542f4;
}
.counter-number {
    font-size: 5rem;
}
.error-input {
    background-color: #e3559a;
    color: #fefefe;
}
</style>