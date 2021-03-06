<template>
    <div class="sideDrawer" :class="{'sideDrawer--show' : show}">
        <div class="sideDrawer__close">
            <button class="closeButton" @click="close">
                <span :class="['material-icons', 'closeButton__icon']">close</span>
            </button>
        </div>

        <button class="project" v-for="path in paths" 
            :key="path.path" 
            @click="routeTo(path.path, path.outside)"
            >
            <p class="project__name">{{ path.title }}</p>
            <span :class="['material-icons', 'project__icon']">chevron_right</span>
        </button>

    </div>
</template>

<script>
    export default {
        name: "SideDrawer",
        props: {
            show: {
                type: Boolean,
                required: true
            }
        },
        emits: ["closeSideDrawer"],
        data() {
            return {
                paths: [
                    {
                        title: 'Todo List',
                        path: 'todo',
                        outside: false
                    },
                    {
                        title: 'Pomodoro Clock',
                        path: 'pomodoro',
                        outside: false
                    },
                    {
                        title: 'Countdown Timer',
                        path: 'countdown',
                        outside: false
                    },
                    {
                        title: 'Weather App',
                        path: 'https://ceoael-weather-app-challenge.herokuapp.com/',
                        outside: true
                    }
                ]
            }
        },
        methods: {
            close() {
                this.$emit('closeSideDrawer');
            },
            routeTo(path, outside) {
                this.close();
                if (outside) {
                    window.open(path, '_blank');
                    return;
                }
                this.$router.push(`/${path}`);
        },
        }
    }
</script>

<style scoped>
* {
    --textColor: #E7E7EB;
    --lightPurple: #1E213A;
    --darkPurple: #100E1D;
}
.sideDrawer {
    position: fixed;
    top: 0;
    left: 0;

    min-height: 100%;
    width: 100%;
    padding: 15px;

    color: var(--textColor);
    background: var(--lightPurple);

    z-index: 999;

    transform: translateX(-100%);   
    transition: .3s transform ease-in-out;
}
.sideDrawer--show {
    transform: translateX(0);
}
.sideDrawer__close {
    display: flex;
    justify-content: flex-end;
    margin-bottom: 38px;
}
.closeButton {
    display: flex;
    padding: 5px;

    background: transparent;
    border: none;   
    border-radius: 5px; 
    cursor: pointer;

    transition: .3s background ease-in-out;
}
.closeButton:hover,
.closeButton:active {
    background: rgba(0,0,0,0.5);
}
.closeButton__icon {
    color:#E7E7EB;
}
.project {
    display: flex;
    justify-content: space-between;
    padding: 22px 12px;
    margin-bottom: 16px;
    background: transparent;
    width: 100%;

    border: 2px solid transparent;
    cursor: pointer;

    transition: .3s all ease-in-out;
}
.project:hover {
    border: 2px solid #616475;
}

.project__name {
    font-family: 'Raleway', sans-serif;
    font-weight: 500;
    font-style: normal;
    font-size: 16px;
    color: #E7E7EB;
}
.project__icon {
    color: #616475;
    opacity: 0;
    transition: .3s all ease-in-out;
}
.project:hover .project__icon {
    opacity: 1;
}

@media (min-width: 800px) {
    .sideDrawer {
        width: 460px;
    }
}
</style>
