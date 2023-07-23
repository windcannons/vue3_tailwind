<script
    setup
    lang="ts">
import {
    onMounted,
    reactive,
    ref
} from "vue";

let userinfo = ref("")
let usertext = '一个勤勤恳恳、认真负责的前端开发工程师，目前居住在上海。'
let num = ref(0)
let IsScroll = ref(false)
let topnav = reactive([
    {
        name: "网站首页",
        href: "#top"
    }, {
        name: "个人简历",
        href: "#me"
    }, {
        name: "求学和工作",
        href: "#experienced"
    }, {
        name: "专业技能",
        href: "#skill"
    }, {
        name: "服务项目",
        href: "#offer"
    }, {
        name: "精选作品",
        href: "#myOpus"
    }, {
        name: "联系我",
        href: "#contect"
    }
])
let current = ref(0)
//   头部结束
//   基本信息开始
let IsTopMove = ref(false)
let imgMove = ref(false)
let userMove = ref(false)
let isChangeImg = ref(false)
let winWidth = ref(0)
//   基本信息结束
// 求学和工作经历开始
let scrollTitle = ref(false)
let scrollContent = ref(false)
//   求学和工作经历结束
//   专业技能开始
let scrollSkill = ref(false)
//   专业技能结束
//   提供服务开始
let offerTop = ref(false)
let offerContent1 = ref(false)
let offerContent2 = ref(false)
//   提供服务结束
//   我的作品开始
let myOpusTop = ref(false)
let myOpusContent = ref(false)
let promptleft = ref("")
let prompttop = ref("")
let moveNum = ref(0)
//   我的作品结束
//   联系我开始
let contectTop = ref(false)
let contectContent = ref(false)
//   联系我结束
//   回到顶部
let isscroll = ref(false)
let isListBox = ref(true)
const riImgBox = ref(null);
const myOpusContents = ref(null);
const MainBox = ref(null);
const Experienced = ref(null);
const Skills = ref(null);
const Offer = ref(null);
const MyOpus = ref(null);
const Contect = ref(null);
const AppMain = ref(null);
const AppList = ref(null);
const ImgBoxs = ref(null);
onMounted(() => {
    // 图片盒子旋转
    const riImg = riImgBox.value as HTMLElement;
    riImg.style.height = riImg.offsetWidth + "px"
    // 我的作品
    const myOpusConten = myOpusContents.value as HTMLElement;
    myOpusConten.style.height = myOpusConten.offsetWidth + "px"
    // 头部开始
    let time = setInterval(() => {
        userinfo.value += usertext[num.value]
        num.value++
        if (num.value === usertext.length) {
            clearInterval(time)
        }
    }, 100)
    // 所有页面滚动事件
    window.onscroll = () => {
        // 头部开始
        winWidth.value = window.innerWidth
        IsScroll.value = window.pageYOffset > 70;
        isscroll.value = window.pageYOffset > 400;
        if (window.pageYOffset < 260) {
            current.value = 0
        }
        // 头部结束
        //  基本信息开始
        const MainBoxs = MainBox.value as HTMLElement;
        let difference = window.pageYOffset - MainBoxs.offsetTop
        if (difference >= -801) {
            IsTopMove.value = true
        }
        if (difference >= -550) {
            current.value = 1

            imgMove.value = true
        }
        if (difference >= -400) {
            userMove.value = true
        }
        // 基本信息结束
        // 求学和工作经历开始
        const Experience = Experienced.value as HTMLElement;
        let experienced = window.pageYOffset - Experience.offsetTop
        if (experienced >= -800) {
            scrollTitle.value = true
        }
        if (experienced >= -500) {
            current.value = 2
        }
        if (experienced >= -300) {
            scrollContent.value = true
        }
        //   求学和工作经历结束
        //   专业技能开始
        const skills = Skills.value as HTMLElement;
        let skill = window.pageYOffset - skills.offsetTop
        if (skill > -600) {
            scrollSkill.value = true
            current.value = 3
        }
        //   专业技能结束
        //   提供服务开始
        const offers = Offer.value as HTMLElement;
        let offer = window.pageYOffset - offers.offsetTop
        if (offer > -600) {
            offerTop.value = true
        }
        if (offer > -400) {
            current.value = 4
            offerContent1.value = true
        }
        if (offer > -100) {
            offerContent2.value = true
        }
        //   提供服务结束
        //   我的作品开始
        const myOpuss = MyOpus.value as HTMLElement;
        let myOpus = window.pageYOffset - myOpuss.offsetTop
        if (myOpus > -600) {
            myOpusTop.value = true
        }
        if (myOpus > -500) {
            current.value = 5
        }
        if (myOpus > -300) {
            myOpusContent.value = true
        }
        //   我的作品结束
        //   联系我开始
        const Contects = Contect.value as HTMLElement;
        let contect = window.pageYOffset - Contects.offsetTop
        if (contect > -600) {
            contectTop.value = true
        }
        if (contect > -400) {
            current.value = 6
            contectContent.value = true
        }
        //   联系我结束
    }
})

function goTop() {
    window.scrollTo({
        top: 0,
        // 平滑移动
        behavior: 'smooth'
    })
}

function listbox() {
    isListBox.value = false
    const appMain = AppMain.value as HTMLElement;
    const appList = AppList.value as HTMLElement;
    appMain.style.left = "-100%"
    appList.style.left = "0"
}

function closeList() {
    isListBox.value = true
    const appMain = AppMain.value as HTMLElement;
    const appList = AppList.value as HTMLElement;
    appMain.style.transition = ".5s"
    appList.style.transition = ".5s"
    appMain.style.left = "0"
    appList.style.left = "100%"
}

function goMain() {
    isListBox.value = true
    const appMain = AppMain.value as HTMLElement;
    const appList = AppList.value as HTMLElement;
    appMain.style.transition = "0s"
    appList.style.transition = "0s"
    appMain.style.left = "0"
    appList.style.left = "100%"
}

//   我的简历图片旋转
function revolve(e) {
    const ImgBox = ImgBoxs.value as HTMLElement;
    const Introduce = MainBox.value as HTMLElement;
    if (window.innerWidth > 990) {
        let x = (e.clientX - Introduce.offsetLeft - ImgBox.offsetWidth / 2) / 10
        let y = (e.clientY - Introduce.offsetTop - Introduce.scrollTop - ImgBox.offsetHeight / 2 + 770) / 10
        if (x > 13) {
            x = 13
        } else if (x < -13) {
            x = -13
        }
        if (y > 15) {
            y = 15
        } else if (y < -15) {
            y = -15
        }
        ImgBox.style.transform = `rotateX(${-y}deg) rotateY(${x}deg)`
    } else {
        ImgBox.style.transform = `rotateX(0deg) rotateY(0deg)`
    }
}

// 我的作品提示
function promptLis(e) {
    moveNum.value = parseInt(e.target.dataset.num)
    promptleft.value = e.offsetX + "px"
    prompttop.value = e.offsetY + 25 + "px"
}
</script>

<template>
    <div
            id="app"
            class="relative overflow-hidden"
            ref="app"
            @mousemove="revolve">
        <!--    appMain    -->
        <div
                class="appMain"
                ref="AppMain">
            <!--    头部-->
            <!--            top-->
            <div
                    class="overflow-hidden relative"
                    id="top">
                <!--                waves-->
                <div
                        class="absolute left-0 top-0 right-0 bottom-0"></div>
                <!--                listbox-->
                <div
                        class=" fixed cursor-pointer z-99999 top-[10px] right-[10px] w-[44px] h-[44px] hidden bg-gray-900 bg-opacity-20 text-center rotate-[10px]"
                        @click="listbox"
                        v-if="isListBox">
                    <img
                            class="w-[20px] h-[20px]"
                            src="./assets/list.png"
                            alt="">
                </div>
                <!--                mainbox-->
                <div
                        class="w-screen h-screen bg-[url('https://ccdn.goodq.top/caches/a8a4b02…/aHR0cHM6Ly81ZGM1MTAyYWJiZjFhLnQ3NC5xaWZlaXllLmNvbS9xZnktY29udGVudC91cGxvYWRzLzIwMTkvMTEvMzAxMGQ5ODAxMjA1YmE2YmVlNjA5Y2Y3MGU2YjMwNDUtOTAud2VicA_p_p100_p_3D_p_p100_p_3D.webp')] bg-no-repeat bg-center bg-cover flex flex-col">
                    <!--                    topbox-->
                    <div
                            class="w-screen h-[70px] pl-[40px] pr-[40px] border-b-1 border-solid border-white border-opacity-10 flex items-center justify-center"
                            style="z-index: 9999"
                            :class="IsScroll?'w-screen bg-white bg-opacity-90 h-[58px] fixed left-0 shadow-md':''">
                        <!--                        TopMain-->
                        <div
                                class="w-[1190px] flex items-center justify-between text-white">
                            <!--                            le -->
                            <h1
                                    class="text-3xl font-f5f487082c474e4472d76201c069f2098 text-white relative"
                                    :class="IsScroll?'text-orange-600':''">
                                Liu
                                Chao
                            </h1>
                            <!--                            ri -->
                            <ul
                                    class="w-[650px] text-base flex justify-around items-center"
                                    :class="IsScroll?'text-gray-700':''">
                                <li
                                        v-for="({href, name},index) in topnav"
                                        :key="index">
                                    <a
                                            class="text-white hover:text-yellow-700"
                                            :href="href"
                                            @click="current=index"
                                            :class="IsScroll?'text-black':''"
                                    >
                                      <span :class="current===index?'text-yellow-700':''">
                                          {{
                                          name
                                          }}
                                      </span>
                                    </a>
                                </li>
                            </ul>
                        </div>
                    </div>
<!--                    userbox-->
                    <div
                            class="flex-1 w-full flex items-center justify-center z-999"
                            :class="IsScroll?'mt-[50px]':''">
<!--                        main-->
                        <div
                                class="h-[330px] w-[1200px] flex flex-col items-center text-white">
                            <img
                                class="w-[220px] h-[220px] rounded-full"
                                    src="./assets/userimg.png"
                                    alt="">
                            <h1 class="text-3xl mt-[22px]">
                                刘&nbsp;超</h1>
                            <p class="text-center px-4 text-base mt-10">
                                {{
                                userinfo
                                }}</p>
                        </div>
                    </div>
                </div>
            </div>
            <!--    基本信息和自我介绍-->
<!--            Introduce-->
            <div
                    class="Introduce"
                    ref="Introduce"
                    id="me">
                <div
                        class="MainBox"
                        ref="MainBox">
                    <!--      头部-->
                    <div
                            class="top"
                            :class="IsTopMove?'topmove':''">
                        <h1>
                            我的简介</h1>
                        <div
                                class="line"></div>
                        <p>
                            我的基本信息和一些自我介绍</p>
                    </div>
                    <!--      内容-->
                    <div
                            class="Content"
                            ref="imgContent">
                        <div
                                class="ImgBox"
                                :class="imgMove?'imgMove':''">
                            <div
                                    class="imgrotate"
                                    @dblclick="isChangeImg = ! isChangeImg"
                                    ref="ImgBoxs">
                                <img
                                        src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fsafe-img.xhscdn.com%2Fbw1%2F705c4d82-1957-4688-a26b-b41ca0ffe3d4%3FimageView2%2F2%2Fw%2F1080%2Fformat%2Fjpg&refer=http%3A%2F%2Fsafe-img.xhscdn.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1685540110&t=8345049e649712952b4fd59bc20c366c"
                                        class="imgMain"
                                        alt="">
                                <div
                                        class="changeBox"
                                        :class="isChangeImg?'isChangeImg':'noChangeImg'"
                                >
                                    <img
                                            :class="isChangeImg?'isHeaderImg':'noHeaderImg'"
                                            src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fsafe-img.xhscdn.com%2Fbw1%2Fe3d5193f-753a-4ad3-8c67-f33395679ba6%3FimageView2%2F2%2Fw%2F1080%2Fformat%2Fjpg&refer=http%3A%2F%2Fsafe-img.xhscdn.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1685154653&t=8f28b569c3301032858b9ebfa33b6ea4"
                                            alt="">
                                </div>
                            </div>
                        </div>
                        <div
                                class="UserMain"
                                :class="userMove?'userMove':''">
                            <div
                                    class="userText">
                                <h3>
                                    基本信息和自我介绍</h3>
                                <h5>
                                    我是一名<span>前端开发工程师</span>目前居住在<span>上海</span>。
                                </h5>
                                <p>
                  <span>
                  物联网应用技术专业,擅长使用HTML、CSS、JavaScript等技术进行网站和Web应用程序的开发。我熟练掌握React、Vue、Angular等流行的前端框架，并有丰富的开发经验。我能够熟练地使用Git、Webpack、Npm等工具，并使用Sass、Less等CSS预处理器进行CSS样式的定制。我相信，在我优秀的技术能力和团队协作能力，以及对前端开发的热情和追求下，我能为公司带来更多的价值。
                </span>
                                </p>
                            </div>
                            <div
                                    class="UserInp">
                                <ul
                                        class="inpList">
                                    <Li>
                                        名称：<span>刘超</span>
                                    </Li>
                                    <Li>
                                        出生日期：<span>2001/03/03</span>
                                    </Li>
                                    <Li>
                                        名族：<span>汉族</span>
                                    </Li>
                                    <Li>
                                        手机：
                                        <span>
                    <a
                            href="tel:17581724627"
                            v-if="winWidth<990">17581724627
                    </a>
                  </span>
                                        <span
                                                v-if="winWidth>990">17581724627</span>
                                    </Li>
                                    <Li>
                                        毕业院校：<span>成都工业职业技术学院</span>
                                    </Li>
                                    <Li>
                                        邮箱：<span>2717741632@qq.com</span>
                                    </Li>
                                    <Li>
                                        籍贯：<span>四川南充</span>
                                    </Li>
                                    <Li>
                                        现居城市：<span>上海市奉贤区</span>
                                    </Li>
                                </ul>
                                <ul
                                        class="icons">
                                    <li>
                                        <img
                                                src="./assets/微信图片_20230504182903.jpg"
                                                alt="">
                                    </li>
                                    <li>
                                        <img
                                                src="./assets/微信图片_20230504182712.jpg"
                                                alt="">
                                    </li>
                                    <li></li>
                                    <li></li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <!--  求学和工作经历-->
            <div
                    class="experienced"
                    id="experienced">
                <div
                        class="w">
                    <div
                            class="top"
                            ref="Experienced">
                        <div
                                class="topBox"
                                :class="scrollTitle?'scrollTitle':''">
                            <div
                                    class="title">
                                <h1>
                                    求学和工作经历</h1>
                                <div
                                        class="wire"></div>
                            </div>
                            <p>
                                无论是求学还是工作，我都在不断学习和成长。持续关注最新技术，尝试新思路，始终保持热情和耐心。</p>
                        </div>
                    </div>
                    <div
                            class="main">
                        <div
                                class="le mainBox"
                                :class="scrollContent?'scrollContentle':''">
                            <div
                                    class="head">
                                <p>
                                    求学经历</p>
                                <div
                                        class="wire"></div>
                            </div>
                            <div
                                    class="content">
                                <ul>
                                    <li>
                                        <div
                                                class="time">
                                            2020
                                        </div>
                                        <div
                                                class="partition">
                                            <div
                                                    class="ball"></div>
                                            <div
                                                    class="line"></div>
                                        </div>
                                        <div
                                                class="text">
                                            <h2>
                                                HTML、CSS、JavaScript</h2>
                                            <span>成都工业职业技术学院</span>
                                            <p>
                                                HTML、CSS、JavaScript是Web开发的基本技能，学习它们可以让我们搭建出漂亮、实用、交互丰富的网站和应用</p>
                                        </div>
                                    </li>
                                    <li>
                                        <div
                                                class="time">
                                            2020
                                        </div>
                                        <div
                                                class="partition">
                                            <div
                                                    class="ball"></div>
                                            <div
                                                    class="line"></div>
                                        </div>
                                        <div
                                                class="text">
                                            <h2>
                                                jQuery</h2>
                                            <span>成都工业职业技术学院</span>
                                            <p>
                                                jQuery是一款强大的JavaScript库，学习了它的选择器、DOM操作、动画效果、事件处理等基本功能，提升Web前端开发效率和用户体验。</p>
                                        </div>
                                    </li>
                                    <li>
                                        <div
                                                class="time">
                                            2021
                                        </div>
                                        <div
                                                class="partition">
                                            <div
                                                    class="ball"></div>
                                            <div
                                                    class="line"></div>
                                        </div>
                                        <div
                                                class="text">
                                            <h2>
                                                Vue</h2>
                                            <span>成都工业职业技术学院</span>
                                            <p>
                                                Vue是一款流行的JavaScript框架，用于构建Web界面和应用程序。它提供了响应式数据绑定、组件化和简洁的语法，使开发过程更加容易和高效。</p>
                                        </div>
                                    </li>
                                </ul>
                            </div>
                        </div>
                        <div
                                class="ri mainBox"
                                :class="scrollContent?'scrollContentri':''">
                            <div
                                    class="head">
                                <p>
                                    工作经历</p>
                                <div
                                        class="wire"></div>
                            </div>
                            <div
                                    class="content">
                                <ul>
                                    <li>
                                        <div
                                                class="time">
                                            2022
                                        </div>
                                        <div
                                                class="partition">
                                            <div
                                                    class="ball"></div>
                                            <div
                                                    class="line"></div>
                                        </div>
                                        <div
                                                class="text">
                                            <h2>
                                                乐享商城</h2>
                                            <span>成都乐云科技有限公司</span>
                                            <p>
                                                提供官方自营的多样化商品，可享官方售后服务、优惠活动及专业建议的购物平台</p>
                                        </div>
                                    </li>
                                    <li>
                                        <div
                                                class="time">
                                            2022
                                        </div>
                                        <div
                                                class="partition">
                                            <div
                                                    class="ball"></div>
                                            <div
                                                    class="line"></div>
                                        </div>
                                        <div
                                                class="text">
                                            <h2>
                                                教学管理系统</h2>
                                            <span>成都乐云科技有限公司</span>
                                            <p>
                                                针对教学管理，包含表单、图标搭建的一个
                                                less
                                                平台，便于管理学生信息；</p>
                                        </div>
                                    </li>
                                    <li>
                                        <div
                                                class="time">
                                            2023
                                        </div>
                                        <div
                                                class="partition">
                                            <div
                                                    class="ball"></div>
                                            <div
                                                    class="line"></div>
                                        </div>
                                        <div
                                                class="text">
                                            <h2>
                                                用户中心</h2>
                                            <span>成都乐云科技有限公司</span>
                                            <p>
                                                负责
                                                Web
                                                页面的开发及交互，与产品设计人员、后台开发人员、测试人员沟通实现产品功能与
                                                操作流程，保障项目的按时交付。</p>
                                        </div>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <!--  专业技能-->
            <div
                    class="skill"
                    id="skill"
                    ref="Skills">
                <div
                        class="w">
                    <div
                            class="le"
                            :class="scrollSkill?'scrollSkillle':''">
                        <div
                                class="topText">
                            <h1>
                                专业技能</h1>
                            <div
                                    class="line"></div>
                        </div>
                        <p>
                            精通HTML/CSS/JavaScript/Vue等前端技术，熟悉跨端开发、性能优化、工程化等工作，有大型项目开发经验，能够提供高质量解决方案和代码实现。
                        </p>
                        <ul>
                            <li>
                                <div
                                        class="top">
                                    <span>HTML、CSS、JavaScript</span>
                                    <span>95%</span>
                                </div>
                                <div
                                        class="progressBox">
                                    <div
                                            class="progress"
                                            :class="scrollSkill?'progresss':''"></div>
                                </div>
                            </li>
                            <li>
                                <div
                                        class="top">
                                    <span>Vue+Vant</span>
                                    <span>92%</span>
                                </div>
                                <div
                                        class="progressBox">
                                    <div
                                            class="progress"
                                            :class="scrollSkill?'progresss':''"></div>
                                </div>
                            </li>
                            <li>
                                <div
                                        class="top">
                                    <span>微信小程序</span>
                                    <span>90%</span>
                                </div>
                                <div
                                        class="progressBox">
                                    <div
                                            class="progress"
                                            :class="scrollSkill?'progresss':''"></div>
                                </div>
                            </li>
                            <li>
                                <div
                                        class="top">
                                    <span>uniapp</span>
                                    <span>94%</span>
                                </div>
                                <div
                                        class="progressBox">
                                    <div
                                            class="progress"
                                            :class="scrollSkill?'progresss':''"></div>
                                </div>
                            </li>
                        </ul>
                    </div>
                    <div
                            class="ri"
                            ref="riImgBox"
                            :class="scrollSkill?'scrollSkillri':''">
                        <div
                                class="container">
                            <div
                                    class="item">
                                <img
                                        src="https://t7.baidu.com/it/u=750454934,606048835&fm=193&f=GIF"
                                        alt="">
                            </div>
                            <div
                                    class="item">
                                <img
                                        src="https://t7.baidu.com/it/u=1153548504,2493654458&fm=193&f=GIF"
                                        alt="">
                            </div>
                            <div
                                    class="item">
                                <img
                                        src="https://t7.baidu.com/it/u=3899972975,794412225&fm=193&f=GIF"
                                        alt="">
                            </div>
                            <div
                                    class="item">
                                <img
                                        src="https://t7.baidu.com/it/u=3026416569,2696284725&fm=193&f=GIF"
                                        alt="">
                            </div>
                            <div
                                    class="item">
                                <img
                                        src="https://t7.baidu.com/it/u=693761745,3063141380&fm=193&f=GIF"
                                        alt="">
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <!--    我可以提供的服务-->
            <div
                    class="offer"
                    id="offer"
                    ref="Offer"
            >
                <div
                        class="w">
                    <div
                            class="top">
                        <div
                                class="topBox"
                                :class="offerTop?'offerTop':''">
                            <div
                                    class="title">
                                <h1>
                                    我的擅长</h1>
                                <div
                                        class="wire"></div>
                            </div>
                            <p>
                                我能为您提供前端开发方案、网站设计、用户体验优化、交互效果制作、响应式布局、浏览器兼容性支持等服务。</p>
                        </div>
                    </div>
                    <div
                            class="content">
                        <ul>
                            <li
                                    :class="offerContent1?'offerContent1':''">
                                <img
                                        src="./assets/li01.png"
                                        alt="">
                                <h4>
                                    网页设计定制</h4>
                                <p>
                                    提供定制化的网站设计服务，以满足您的特定业务需求和用户体验
                                </p>
                            </li>
                            <li
                                    :class="offerContent1?'offerContent1':''">
                                <img
                                        src="./assets/li02.png"
                                        alt="">
                                <h4>
                                    界面开发</h4>
                                <p>
                                    开发易用、美观、直观的用户界面，提高您网站的用户满意度。</p>
                            </li>
                            <li
                                    :class="offerContent1?'offerContent1':''">
                                <img
                                        src="./assets/li03.png"
                                        alt="">
                                <h4>
                                    响应式设计</h4>
                                <p>
                                    创建针对不同设备的响应式设计，确保您的网站在手机、平板和桌面电脑上都能完美显示。</p>
                            </li>
                            <li
                                    :class="offerContent2?'offerContent2':''">
                                <img
                                        src="./assets/li04.png"
                                        alt="">
                                <h4>
                                    网站重构</h4>
                                <p>
                                    帮助您更新老旧的网站，优化网站结构，使其更易于使用和管理。</p>
                            </li>
                            <li
                                    :class="offerContent2?'offerContent2':''">
                                <img
                                        src="./assets/li05.png"
                                        alt="">
                                <h4>
                                    SEO优化</h4>
                                <p>
                                    对您的网站进行搜索引擎优化，提高其在搜索引擎中的排名</p>
                            </li>
                            <li
                                    :class="offerContent2?'offerContent2':''">
                                <img
                                        src="./assets/li06.png"
                                        alt="">
                                <h4>
                                    数据可视化设计</h4>
                                <p>
                                    利用现有的数据可视化库和工具，对数据进行分析和可视化处理，帮助企业更好地理解和利用数据。</p>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
            <!--    我的作品-->
            <div
                    class="myOpus"
                    id="myOpus"
                    ref="MyOpus"
            >
                <div
                        class="w">
                    <div
                            class="top">
                        <div
                                class="topBox"
                                :class="myOpusTop?'myOpusTop':''">
                            <div
                                    class="title">
                                <h1>
                                    我的作品</h1>
                                <div
                                        class="wire"></div>
                            </div>
                            <p>
                                我的作品都注重用户需求和体验，会根据产品的定位和特点，开发适合的功能，让用户在界面操作时流畅自如。同时，我还会根据不同设备和分辨率，进行响应式设计，确保用户可以在各种环境下获得一致的使用体验。</p>
                        </div>
                    </div>
                    <div
                            class="content"
                            ref="myOpusContents"
                            :class="myOpusContent?'myOpusContent':''"
                            @mousemove="promptLis"
                    >
                        <ul>
                            <li>
                                <a
                                        data-num="1"
                                        href="http://2717741632.web3v.work/time/">
                                    <div
                                            v-show="moveNum===1"
                                            :style="{left:promptleft,top:prompttop}">
                                        时钟
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a
                                        data-num="2"
                                        href="http://2717741632.web3v.work/baidu/">
                                    <div
                                            v-show="moveNum===2"
                                            :style="{left:promptleft,top:prompttop}">
                                        百度页面
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a
                                        data-num="3"
                                        href="http://17581724627.web3v.vip/design/">
                                    <div
                                            v-show="moveNum===3"
                                            :style="{left:promptleft,top:prompttop}">
                                        轮滑招生网
                                    </div>
                                </a>
                            </li>
                            <li>
                                <!-- 华为移动端商城-->
                                <a
                                        data-num="4"
                                        href="http://13108179070.web3v.work/dist/">
                                    <div
                                            v-show="moveNum===4"
                                            :style="{left:promptleft,top:prompttop}">
                                        华为移动端商城
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a
                                        data-num="5"
                                        href="http://17581724627.web3v.vip/tea/index.html">
                                    <div
                                            v-show="moveNum===5"
                                            :style="{left:promptleft,top:prompttop}">
                                        茶商城
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a
                                        data-num="6"
                                        href="http://13108179070.web3v.work/tiamnao//">
                                    <div
                                            v-show="moveNum===6"
                                            :style="{left:promptleft,top:prompttop}">
                                        天猫网页商城
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a
                                        data-num="7"
                                        href="http://2717741632.web3v.work/apple/">
                                    <div
                                            v-show="moveNum===7"
                                            :style="{left:promptleft,top:prompttop}">
                                        苹果网页商城
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a
                                        data-num="8"
                                        href="http://2717741632.web3v.work/jdong/">
                                    <div
                                            v-show="moveNum===8"
                                            :style="{left:promptleft,top:prompttop}">
                                        京东网页商城
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a
                                        data-num="9"
                                        href="http://2717741632.web3v.work/dazhong/">
                                    <div
                                            v-show="moveNum===9"
                                            :style="{left:promptleft,top:prompttop}">
                                        大众点评网页
                                    </div>
                                </a>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
            <!--    联系我-->
            <div
                    class="contect"
                    ref="Contect"
                    id="contect">
                <div
                        class="w">
                    <div
                            class="top">
                        <div
                                class="topBox"
                                :class="contectTop?'contectTop':''">
                            <div
                                    class="title">
                                <h1>
                                    联系我</h1>
                                <div
                                        class="wire"></div>
                            </div>
                        </div>
                    </div>
                    <div
                            class="content"
                            :class="contectContent?'contectContent':''">
                        <div
                                class="tr one">
                            <div>
                                <p>
                                    电话：</p>
                                <span
                                        v-if="winWidth>990">17581724627</span>
                                <span>
                  <a
                          href="tel:17581724627"
                          v-if="winWidth<990">17581724627
                    </a>
                </span>
                            </div>
                            <div>
                                <p>
                                    地址：</p>
                                <span>上海市奉贤区</span>
                            </div>
                        </div>
                        <div
                                class="tr one">
                            <div>
                                <p>
                                    QQ：</p>
                                <span>2717741632</span>
                            </div>
                            <div>
                                <p>
                                    微信：</p>
                                <span>lc2717741632</span>
                            </div>
                        </div>
                        <div
                                class="img">
                            <ul>
                                <li>
                                    <p>
                                        QQ</p>
                                    <img
                                            src="./assets/微信图片_20230504182903.jpg"
                                            alt="">
                                </li>
                                <li>
                                    <p>
                                        微信</p>
                                    <img
                                            src="./assets/微信图片_20230504182712.jpg"
                                            alt="">
                                </li>
                            </ul>
                        </div>
                        <div
                                class="submit">
                            <a
                                    href="https://free.3v.do/gbook/post.asp?username=liucha0">给我留言</a>
                        </div>
                    </div>
                </div>
            </div>
            <!--尾部-->
            <div
                    class="footer">
                <h1>
                    Liu&nbsp;Chao</h1>
                <ul>
                    <li>

                    </li>
                    <li>

                    </li>
                    <li>

                    </li>
                    <li>

                    </li>
                    <li>

                    </li>
                </ul>
                <div
                        class="Line"></div>
                <p>
                    ©
                    2019
                    copyright
                    all
                    right
                    reserved</p>
            </div>
            <!--    回到顶部-->
            <div
                    class="goTop"
                    v-show="isscroll"
                    @click="goTop">
                <img
                        src="./assets/goTop.png"
                        alt="">
            </div>
        </div>
        <div
                class="appList"
                ref="AppList">
            <div
                    class="top">
        <span
                @click="closeList">
        ×
      </span>
            </div>
            <ul>
                <li
                        v-for="({href, name},index) in topnav"
                        @click="goMain"
                        :key="index">
                    <a
                            :href="href"
                            @click="current=index"
                            :class="current===index?'current':''">
                        {{
                        name
                        }}
                    </a>
                </li>
            </ul>
        </div>
    </div>
</template>

<style
    lang="less">
#app {
  position: relative;
  overflow: hidden;
}

//基本信息和自我介绍开始
.Introduce {
  width: 100%;
  height: 904px;
  background-color: #fff;
  padding: 100px 0 200px;

  .MainBox {
    width: 1190px;
    height: 100%;
    margin: 0 auto;

    //头部
    .top {
      transform: translateY(60px);
      visibility: hidden;

      h1 {
        width: 176px;
        height: 65px;
        font-size: 44px;
        font-weight: 400;
        color: #000;
        font-family: f5f487082c474e4472d76201c069f2098, serif;
      }

      .line {
        width: 160px;
        height: 5px;
        background-color: #f7eccb;
        margin: -10px 6px 0;
      }

      p {
        margin-top: 10px;
        height: 24px;
        font-size: 16px;
        color: #828282;
        letter-spacing: 1px;
      }
    }

    .topmove {
      /* 调用画面 */
      animation-name: topmove;
      /* 持续时间 */
      animation-duration: 1s;
      animation-fill-mode: forwards;
    }

    @keyframes topmove {
      0% {
        transform: translateY(60px);
        visibility: visible;
        opacity: .2;
      }
      100% {
        transform: translateY(0);
        visibility: visible;
        opacity: 1;
      }
    }

    //内容
    .Content {
      margin-top: 60px;
      display: flex;
      justify-content: space-between;

      .ImgBox {
        width: 380px;
        height: 448px;
        margin: 0 5px;
        transform: translateX(-150px);
        visibility: hidden;
        transition: .4s;
        animation-timing-function: linear;
        perspective: 1000px;


        .imgrotate {
          width: 100%;
          height: 100%;
          transition: 1.5s;
          position: relative;
          overflow: hidden;
        }

        .isChangeImg {
          animation-name: isChangeImg;
        }

        @keyframes isChangeImg {
          to {
            top: 100%;
          }
        }

        .noChangeImg {
          animation-name: noChangeImg;
        }

        @keyframes noChangeImg {
          from {
            top: 100%;
          }
          to {
            top: 0;
          }
        }

        img {
          width: 100%;
          height: 100%;
          animation-duration: .6s;
          animation-fill-mode: forwards;
        }

        .isHeaderImg {
          animation-name: isHeaderImg;
        }

        .noHeaderImg {
          animation-name: noHeaderImg;
        }

        @keyframes isHeaderImg {
          to {
            top: -100%;
          }
        }
        @keyframes noHeaderImg {
          from {
            top: -100%;
          }
          to {
            top: 0;
          }
        }


        .changeBox {
          animation-duration: .6s;
          animation-fill-mode: forwards;
          width: 100%;
          height: 100%;
          position: absolute;
          top: 0;
          left: 0;
          overflow: hidden;

          img {
            height: 100%;
          }
        }
      }

      .imgMove {
        /* 调用画面 */
        animation-name: imgMove;
        /* 持续时间 */
        animation-duration: 1s;
        animation-fill-mode: forwards;
      }

      @keyframes imgMove {
        0% {
          transform: translateX(-280px);
          opacity: .2;
          visibility: visible;
        }
        100% {
          transform: translateX(0);
          opacity: 1;
          visibility: visible;
        }
      }

      .UserMain {
        flex: 1;
        height: 447px;
        padding-left: 47px;
        color: #000;
        font-family: "微软雅黑", Helvetica, Arial, Verdana, sans-serif;
        font-style: normal;
        transform: translateY(260px);
        visibility: hidden;

        .userText {

          h3 {
            font-size: 22px;
            width: 207px;
            height: 29px;
          }

          h5 {
            font-size: 14px;
            height: 34px;
            margin-top: 15px;

            span {
              color: #febd01;
            }
          }

          p {
            span {
              font-size: 14px;
              margin-top: 4px;
              color: #828282;
              line-height: 28px;
              letter-spacing: 1px;
              background: linear-gradient(to right, #ec695c, #61c454) no-repeat right bottom;
              background-size: 0 2px;
              transition: background-size 1s;
            }

            &:hover span {
              background-position-x: left;
              background-size: 100% 2px;
            }
          }
        }

        .UserInp {
          margin-top: 20px;

          .inpList {
            width: 100%;
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            justify-content: space-between;
            padding: 0 10px;

            li {
              width: 48%;
              height: 52px;
              padding: 15px 0;
              border-bottom: 1px solid #eeeeee;
              font-size: 15px;
              font-weight: 800;
              display: flex;
              align-items: center;

              span {
                font-weight: 400;
                color: #828282;
                margin-left: 5px;

                a {
                  &:hover {
                    color: #828282;
                  }
                }
              }
            }
          }

          .icons {
            height: 32px;
            margin-top: 20px;
            z-index: 999;

            li {
              width: 32px;
              height: 32px;
              float: left;
              margin-right: 10px;
              background: url("https://f.goodq.top/FeiEditor/images/icon/social_icon_32x32.png") no-repeat;
              position: relative;
              cursor: pointer;

              img {
                width: 88px;
                height: 88px;
                position: absolute;
                top: 120%;
                left: -5px;
                transition: .3s;
                opacity: 0;
              }

              &:hover img {
                opacity: 1;
              }

              &:nth-child(1) {
                background-position: -64px, 0;
              }

              &:nth-child(2) {
                background-position: 0, 0;
              }

              &:nth-child(3) {
                background-position: -32px, 0;
              }

              &:nth-child(4) {
                background-position: -128px, 0;
              }
            }
          }
        }
      }

      .userMove {
        /* 调用画面 */
        animation-name: userMove;
        /* 持续时间 */
        animation-duration: .6s;
        animation-fill-mode: forwards;
      }

      @keyframes userMove {
        0% {
          transform: translateY(280px);
          visibility: visible;
          opacity: .2;
        }
        100% {
          transform: translateX(0);
          visibility: visible;
          opacity: 1;
        }
      }
    }
  }
}

//基本信息和自我介绍结束
//求学和工作经历开始
@media (max-width: 990px) {
  .experienced {
    height: auto !important;
    padding-bottom: 40px;
    overflow: hidden;
  }
}

.experienced {
  overflow: hidden;
  width: 100%;
  height: 1036px;
  background-color: #f5f8fd;
  padding-top: 100px;

  .w {
    width: 1200px;
    margin: 0 auto;
  }

  .scrollTitle {
    /* 调用画面 */
    animation-name: scrollTitle;
    /* 持续时间 */
    animation-duration: 1s;
    animation-fill-mode: forwards;
  }

  @keyframes scrollTitle {
    0% {
      transform: translateY(90px);
      visibility: visible;
      opacity: .2;
    }
    100% {
      transform: translateY(0);
      visibility: visible;
      opacity: 1;
    }
  }

  .top {
    overflow: hidden;
    visibility: hidden;

    .topBox {
      display: flex;
      flex-direction: column;
      align-items: center;
      transform: translateY(60px);
    }

    .title {
      width: 308px;
      height: 65px;

      h1 {

        font-size: 44px;
        font-weight: 400;
        color: #000;
        font-family: f5f487082c474e4472d76201c069f2098, serif;
      }

      .wire {
        width: 300px;
        height: 5px;
        background-color: #f9e5a8;
        margin: -13px 4px 0;
      }
    }

    p {
      font-size: 15px;
      color: #828282;
      height: 77px;
      padding: 20px 0 33px;
    }
  }

  @media (max-width: 1200px) {
    .main {
      margin: 0 20px;
    }

    .w {
      width: 100% !important;
    }

    .content ul {
      padding: 30px 20px 20px !important;
    }
  }

  @media (max-width: 990px) {
    .top p {
      width: 100%;
      text-align: center;
      padding: 0 25px;
      margin-top: 25px;
    }

    .main {
      width: 100%;
      height: auto !important;
    }

    .mainBox {
      width: 100% !important;
      height: auto !important;
      padding: 0 35px 0 15px !important;
    }

    .w {
      width: 100% !important;
      padding: 0 20px;
    }

    .content ul {
      padding: 30px 20px 20px !important;
      height: auto !important;

      li {
        padding: 20px 0 0;
      }
    }

    .text {
      flex: 0.9;
    }

    .ri {
      margin-top: 28px;
    }

    .line {
      height: 100px !important;
    }
  }


  .main {
    height: 638px;
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;

    .scrollContentle {
      animation-name: scrollContentle;
    }

    .scrollContentri {
      animation-name: scrollContentri;
    }

    @keyframes scrollContentle {
      0% {
        transform: translateX(-350px);
        visibility: visible;
        opacity: .2;
      }
      100% {
        transform: translateX(0);
        visibility: visible;
        opacity: 1;
      }
    }
    @keyframes scrollContentri {
      0% {
        transform: translateX(350px);
        visibility: visible;
        opacity: .2;
      }
      100% {
        transform: translateX(0);
        visibility: visible;
        opacity: 1;
      }
    }

    .mainBox {
      visibility: hidden;
      animation-duration: .8s;
      animation-fill-mode: forwards;
      animation-timing-function: ease;
      width: 50%;
      height: 638px;
      padding: 0 25px 0 5px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;

      .head {
        width: 100%;
        height: 39px;

        p {
          font-size: 20px;
          width: 80px;
          margin-bottom: 5px;
          color: #000;
          font-weight: 800;
        }

        .wire {
          width: 80px;
          height: 1px;
          background-color: #fad363;
        }
      }

      .content {
        width: 100%;
        flex: 1;
        background-color: #fff;
        margin-top: 24px;

        ul {
          padding: 30px 40px 20px;
          width: 100%;
          height: 100%;
          display: flex;
          flex-direction: column;
          justify-content: space-between;

          li {
            display: flex;
            justify-content: space-around;
            height: 30%;
            width: 100%;
            border-bottom: 1px solid #f7f7f7;
            padding-bottom: 20px;

            &:nth-child(3) {
              border: none;
            }

            .time {
              width: 82px;
              height: 26px;
              color: #febd01;
              padding: 0 25px 0 5px;
              font-size: 16px;
            }

            .partition {
              margin-right: 15px;
              width: 20px;
              height: 100%;
              position: relative;

              .ball {
                width: 20px;
                height: 20px;
                border-radius: 50%;
                background-color: #fcbd00;
                border: 1px solid #000;
                position: absolute;
                top: 0;
                left: 0;
              }

              .line {
                width: 1px;
                height: 100%;
                margin: 0 auto;
                background-color: #f0f0f0;
              }
            }

            .text {
              width: 320px;
              height: 100%;

              h2 {
                font-size: 18px;
                font-family: f5f487082c474e4472d76201c069f2098, serif;
                color: #000;
              }

              span {
                font-size: 12px;
                color: #828282;
              }

              p {
                font-size: 14px;
                color: #828282;
                margin-top: 20px;
              }
            }
          }
        }
      }
    }
  }
}

//求学和工作经历结束
//专业技能开始


@media (max-width: 990px) {
  .skill {
    height: auto !important;
    padding: 43px 0 66px;

    .w {
      width: 100% !important;
      height: auto !important;
      justify-content: center !important;

      .line {
        margin-left: 48px;
      }

      h1 {
        text-align: center;
      }

      p {
        text-align: center;
      }

      .le {
        width: 100% !important;
        margin-bottom: 25px;

        ul {
          width: 100% !important;
        }
      }

      .ri {
        width: 290px !important;
      }
    }
  }
}

@media (max-width: 1200px) {
  #app #skill .w .ri {
    width: 330px;
    height: 330px;
  }
}

.skill {
  overflow: hidden;
  height: 826px;
  display: flex;
  align-items: center;
  justify-content: center;
  @media (max-width: 1260px) {
    .w {
      width: 100% !important;
      padding: 0 30px !important;
    }
  }

  .w {
    width: 1190px;
    height: 538px;
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    padding: 0 20px;

    .scrollSkillle {
      animation-name: scrollSkillle;
      animation-duration: 1s;
      animation-fill-mode: forwards;
    }

    @keyframes scrollSkillle {
      0% {
        transform: translateX(-300px);
        visibility: visible;
        opacity: .2;
      }
      100% {
        transform: translateX(0);
        visibility: visible;
        opacity: 1;
      }
    }

    .scrollSkillri {
      animation-name: scrollSkillri;
      animation-duration: 1s;
      animation-fill-mode: forwards;
    }

    @keyframes scrollSkillri {
      0% {
        transform: translateX(300px);
        visibility: visible;
        opacity: .2;
      }
      100% {
        transform: translateX(0);
        visibility: visible;
        opacity: 1;
      }
    }

    .le {
      width: 47%;
      transform: translateX(-300px);
      visibility: hidden;

      @media (max-width: 990px) {
        .topText {
          margin: 0 auto;
        }
      }

      .topText {
        width: 180px;
        height: 65px;

        h1 {
          font-size: 44px;
          color: #000;
          font-weight: 400;
          font-family: f5f487082c474e4472d76201c069f2098, serif;
        }

        .line {
          width: 180px;
          height: 5px;
          background-color: #fbe7aa;
          margin-left: 10px;
          margin-top: -13px;
        }
      }

      p {
        font-size: 15px;
        color: #6f6f6f;
        margin: 20px 0 45px;
        width: 100%;
      }

      ul {
        width: 90%;

        li {
          margin-top: 25px;

          .top {
            height: 24px;
            width: 100%;
            font-size: 16px;
            font-weight: 800;
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 6px;
          }

          .progressBox {
            width: 100%;
            height: 5px;
            background-color: #eeeeee;
            position: relative;

            .progress {
              width: 0;
              position: absolute;
              left: 0;
              top: 0;
              height: 100%;
              background-color: #febd01;
              animation-duration: 1s;
              animation-fill-mode: forwards;
              animation-timing-function: ease;
            }
          }

          @keyframes progress1 {
            to {
              width: 95%;
            }
          }
          @keyframes progress2 {
            to {
              width: 92%;
            }
          }
          @keyframes progress3 {
            to {
              width: 90%;
            }
          }
          @keyframes progress4 {
            to {
              width: 94%;
            }
          }

          &:nth-child(1) .progresss {
            animation-name: progress1;
            animation-delay: .9s;
          }

          &:nth-child(2) .progresss {
            animation-name: progress2;
            animation-delay: 1s;
          }

          &:nth-child(3) .progresss {
            animation-name: progress3;
            animation-delay: 1.1s;
          }

          &:nth-child(4) .progresss {
            animation-name: progress4;
            animation-delay: 1.2s;
          }
        }
      }
    }

    .ri {
      margin-top: 50px;
      margin-right: 20px;
      width: 400px;
      height: 400px;
      transform: translateX(300px);
      visibility: hidden;
      display: flex;
      align-items: center;
      justify-content: center;

      .container {
        width: 100%;
        height: 100%;
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-template-rows: repeat(3, 1fr);
        grid-template:
      "A A B"
      "C D B"
      "C E E";
        gap: 5px;
      }

      .item {
        overflow: hidden;
        border: 2px solid;
        display: flex;
        align-items: center;
        justify-content: center;
      }

      .item:nth-child(1) {
        grid-area: A;
      }

      .item:nth-child(2) {
        grid-area: B;
      }

      .item:nth-child(3) {
        grid-area: C;
      }

      .item:nth-child(4) {
        grid-area: D;
      }

      .item:nth-child(5) {
        grid-area: E;
      }

      .container {
        --r: 360deg;
        animation: rotation 11s linear infinite;
      }

      @media (max-width: 990px) {
        .item img {
          width: 260% !important;
          height: 260% !important;
        }
      }


      .item img {
        --r: -360deg;
        animation: rotation 11s linear infinite;
        width: 235%;
        height: 235%;

      }

      @keyframes rotation {
        to {
          transform: rotate(var(--r));
        }
      }
    }
  }
}

//专业技能开始结束
//我可以提供的服务开始
@media (max-width: 990px) {
  .offer {
    height: auto !important;
    padding-bottom: 45px;
  }
}

.offer {
  overflow: hidden;
  width: 100%;
  height: 1036px;
  background-color: #f5f8fd;
  padding-top: 100px;

  @media (max-width: 1200px) {
    .w {
      width: 100% !important;
    }
  }
  @media (max-width: 990px) {
    .top {
      p {
        text-align: center;
        padding: 20px 20px 33px !important;
        height: auto !important;
      }
    }

    .content {
      height: auto !important;

      li {
        width: 88% !important;
      }
    }
  }

  .w {
    width: 1200px;
    margin: 0 auto;

    .top {
      overflow: hidden;
      text-align: center;

      .offerTop {
        animation-name: offerTop;
        animation-duration: 1s;
        animation-fill-mode: forwards;
      }

      @keyframes offerTop {
        0% {
          transform: translateY(60px);
          visibility: visible;
          opacity: .2;
        }
        100% {
          transform: translateY(0);
          visibility: visible;
          opacity: 1;
        }
      }

      .topBox {
        display: flex;
        visibility: hidden;
        flex-direction: column;
        align-items: center;
        transform: translateY(60px);
      }

      .title {
        width: 201px;
        height: 65px;

        h1 {
          font-size: 44px;
          font-weight: 400;
          color: #000;
          font-family: f5f487082c474e4472d76201c069f2098, serif;
        }

        .wire {
          width: 200px;
          height: 5px;
          background-color: #f9e5a8;
          margin: -10px 1px 0;
        }
      }

      p {
        font-size: 15px;
        color: #828282;
        height: 77px;
        padding: 20px 0 33px;
      }
    }

    .content {
      width: 100%;
      padding: 0 10px;
      margin: 0 auto;
      height: 670px;

      ul {
        display: flex;
        align-items: center;
        justify-content: space-around;
        flex-wrap: wrap;

        .offerContent1 {
          animation-name: offerContent;
          animation-duration: 1s;
          animation-fill-mode: forwards;
        }

        @keyframes offerContent {
          0% {
            transform: translateY(100px);
            visibility: visible;
            opacity: .2;
          }
          100% {
            transform: translateY(0);
            visibility: visible;
            opacity: 1;
          }
        }

        .offerContent2 {
          animation-name: offerContent;
          animation-duration: .8s;
          animation-fill-mode: forwards;
          transform: translateY(100px);
        }

        li {
          transform: translateY(10px);
          visibility: hidden;
          background-color: #fff;
          width: 30%;
          padding: 30px;
          display: flex;
          flex-direction: column;
          align-items: center;
          margin-top: 33px;
          box-shadow: 5px 5px 10px #ccc;
          border: 1px solid #e9e9e9;

          &:nth-child(1) {
            animation-delay: 0.1s;
          }

          &:nth-child(2) {
            animation-delay: 0.3s;
          }

          &:nth-child(3) {
            animation-delay: 0.5s;
          }

          &:nth-child(4) {
            animation-delay: 0.1s;
          }

          &:nth-child(5) {
            animation-delay: 0.3s;
          }

          &:nth-child(6) {
            animation-delay: 0.5s;
          }

          img {
            width: 80px;
            height: 80px;
          }

          h4 {
            font-size: 16px;
            margin-top: 16px;
          }

          h4 {
            font-family: fd721bf845ff7dd1453a0242bf8cd7b2c, sans-serif;
            color: #000;
          }

          p {
            width: 100%;
            text-align: center;
            font-size: 15px;
            color: #828282;
            margin: 20px 0 33px;
            min-height: 67px;
          }
        }
      }
    }
  }
}

//我可以提供的服务结束
//我的作品开始
@media (max-width: 1200px) {
  .myOpus {
    height: auto !important;
    padding-bottom: 145px;
  }
}

@media (max-width: 990px) {
  .myOpus {
    padding-bottom: 40px !important;
  }
}

.myOpus {
  width: 100%;
  height: 1519px;
  background-color: #fff;
  padding-top: 100px;


  @media (max-width: 1200px) {
    .content {
      width: 94% !important;
      //height: auto !important;

      ul {
        width: 100% !important;
      }
    }
  }

  @media (max-width: 990px) {
    .w {
      .top {
        p {
          width: 88%;
        }
      }

      .content {
        width: 80% !important;
      }
    }
  }

  .myOpusTop {
    /* 调用画面 */
    animation-name: myOpusTop;
    /* 持续时间 */
    animation-duration: 1s;
    animation-fill-mode: forwards;
  }

  @keyframes myOpusTop {
    0% {
      transform: translateY(90px);
      visibility: visible;
      opacity: .2;
    }
    100% {
      transform: translateY(0);
      visibility: visible;
      opacity: 1;
    }
  }

  .top {
    overflow: hidden;
    visibility: hidden;

    .topBox {
      display: flex;
      flex-direction: column;
      align-items: center;
      transform: translateY(60px);
    }

    .title {
      width: 180px;
      height: 65px;
      text-align: center;

      h1 {

        font-size: 44px;
        font-weight: 400;
        color: #000;
        font-family: f5f487082c474e4472d76201c069f2098, serif;
      }

      .wire {
        width: 180px;
        height: 5px;
        background-color: #f9e5a8;
        margin: -10px 0 0;
      }
    }

    p {
      width: 900px;
      font-size: 15px;
      color: #828282;
      padding: 20px 0 33px;
      text-align: center;
    }
  }

  .myOpusContent {
    /* 调用画面 */
    animation-name: myOpusContent;
    /* 持续时间 */
    animation-duration: .6s;
    animation-fill-mode: forwards;
  }

  @keyframes myOpusContent {
    0% {
      transform: translateY(200px);
      visibility: visible;
      opacity: .2;
    }
    100% {
      transform: translateY(0);
      visibility: visible;
      opacity: 1;
    }
  }


  .content {
    visibility: hidden;
    transform: translateY(200px);
    width: 1110px;
    height: 1110px;
    margin: 20px auto 0;


    ul {
      padding: 10px;
      width: 1110px;
      height: 100%;
      display: grid;
      --c1: 1fr;
      --c2: 1fr;
      --c3: 1fr;
      --r1: 1fr;
      --r2: 1fr;
      --r3: 1fr;
      grid-template-columns: var(--c1) var(--c2) var(--c3);
      grid-template-rows: var(--r1) var(--r2) var(--r3);
      grid-gap: 10px;
      transition: .5s;
      background-color: antiquewhite;


      &:has(li:nth-child(1):hover) {
        --c1: 2fr;
        --r1: 2fr;
      }

      &:has(li:nth-child(2):hover) {
        --r1: 2fr;
        --c2: 2fr;
      }

      &:has(li:nth-child(3):hover) {
        --r1: 2fr;
        --c3: 2fr;
      }

      &:has(li:nth-child(4):hover) {
        --r2: 2fr;
        --c1: 2fr;
      }

      &:has(li:nth-child(5):hover) {
        --r2: 2fr;
        --c2: 2fr;
      }

      &:has(li:nth-child(6):hover) {
        --r2: 2fr;
        --c3: 2fr;
      }

      &:has(li:nth-child(7):hover) {
        --r3: 2fr;
        --c1: 2fr;
      }

      &:has(li:nth-child(8):hover) {
        --r3: 2fr;
        --c2: 2fr;
      }

      &:has(li:nth-child(9):hover) {
        --r3: 2fr;
        --c3: 2fr;
      }

      li {
        border-radius: 15px;
        background-color: #fff !important;
        //overflow: hidden;
        position: relative;

        a {
          display: block;
          width: 100%;
          height: 100%;
          color: skyblue;

          div {
            height: 30px;
            line-height: 30px;
            padding: 0 15px;
            background-color: #fff;
            border: 1px solid #ccc;
            font-size: 14px;
            border-radius: 5px;
            position: absolute;
            white-space: nowrap;
            z-index: 99;
          }
        }

        &:nth-child(1) {
          background: url("./assets/my1.png") no-repeat center /contain;
        }

        &:nth-child(2) {
          background: url("./assets/my2.png") no-repeat center /contain;
        }

        &:nth-child(3) {
          background: url("./assets/my3.png") no-repeat center /contain;
        }

        &:nth-child(4) {
          background: url("./assets/my4.png") no-repeat center /contain;
        }

        &:nth-child(5) {
          background: url("./assets/my5.png") no-repeat center /contain;
        }

        &:nth-child(6) {
          background: url("./assets/tianmao.png") no-repeat center /contain;
        }

        &:nth-child(7) {
          background: url("./assets/apple.png") no-repeat center /contain;
        }

        &:nth-child(8) {
          background: url("./assets/jdong.png") no-repeat center /contain;
        }

        &:nth-child(9) {
          background: url("./assets/dazhong.png") no-repeat center /contain;
        }
      }
    }
  }
}

//我的作品结束
//联系我开始
@media (max-width: 990px) {
  .contect {
    height: auto !important;
    padding: 50px 0 50px !important;
  }
}

.contect {
  width: 100%;
  height: 870px;
  background-color: #f5f8fd;
  padding-top: 100px;
  @media (max-width: 1280px) {
    .w {
      width: 100% !important;

      p {
        height: auto !important;
      }
    }
  }

  .w {
    width: 1200px;
    padding: 0 40px;
    margin: 0 auto;

    .contectTop {
      animation-name: contectTop;
      /* 持续时间 */
      animation-duration: 1s;
      animation-fill-mode: forwards;
    }

    @keyframes contectTop {
      0% {
        transform: translateY(90px);
        visibility: visible;
        opacity: .2;
      }
      100% {
        transform: translateY(0);
        visibility: visible;
        opacity: 1;
      }
    }

    .top {
      overflow: hidden;
      visibility: hidden;

      .topBox {
        display: flex;
        flex-direction: column;
        align-items: center;
        //transform: translateY(60px);
      }

      .title {
        width: 140px;
        height: 65px;
        text-align: center;

        h1 {

          font-size: 44px;
          font-weight: 400;
          color: #000;
          font-family: f5f487082c474e4472d76201c069f2098, serif;
        }

        .wire {
          width: 140px;
          height: 5px;
          background-color: #f9e5a8;
          margin: -10px 0 0;
        }
      }

    }

    @media (max-width: 990px) {
      .content {
        height: auto !important;

        .topInp {
          height: 115px !important;

          input {
            width: 99% !important;
            height: 40% !important;
          }
        }
      }
    }

    .contectContent {
      animation-name: contectTop;
      /* 持续时间 */
      animation-duration: 1s;
      animation-fill-mode: forwards;
    }

    @media (max-width: 990px) {
      .content {
        padding: 10px !important;
        height: auto !important;
      }
    }

    .content {
      visibility: hidden;
      overflow: hidden;
      width: 100%;
      height: 520px;
      box-shadow: 5px 5px 20px #dddddd;
      margin-top: 40px;
      padding: 50px;
      border: 1px solid #e0e3e7;
      background: #fff url("https://ccdn.goodq.top/caches/a8a4b02e7048697ffdf7bfb95c81ad71/aHR0cHM6Ly81ZGM1MTAyYWJiZjFhLnQ3NC5xaWZlaXllLmNvbS9xZnktY29udGVudC91cGxvYWRzLzIwMTkvMTEvNjBmYWQxYmI2MjA0NmE5N2VlMDE3ODBjNGE0MjliYzQtOTAud2VicA_p_p100_p_3D_p_p100_p_3D.webp") no-repeat right top;
      @media (max-width: 990px) {
        .tr {
          height: 100% !important;
        }

        .one {
          div {
            width: 90% !important;
            font-size: 16px !important;
            font-weight: 400 !important;
            margin-top: 10px;

            span {
              font-size: 16px !important;
            }
          }
        }
      }

      .one {
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: space-between;
      }

      .tr {
        width: 100%;
        height: 50px;
        font-size: 25px;
        font-weight: 800;
        font-family: f5f487082c474e4472d76201c069f2098, serif;
        color: #000;

        div {
          display: flex;
          width: 50%;

          p {
            width: 80px;
            height: 100%;
          }

          span {
            color: #101010;

            a {
              &:hover {
                color: #101010;
              }
            }
          }
        }


      }

      @keyframes submit {
        to {
          background-position: -400% 0;
        }
      }

      ul {
        margin-top: 15px;
        width: 50%;
        display: flex;
        align-items: center;
        justify-content: space-between;
        @media (max-width: 990px) {
          p {
            font-size: 18px !important;
            font-weight: 400 !important;
          }
        }

        li {
          width: 48%;
          display: flex;
          flex-direction: column;
          align-items: center;

          p {
            font-size: 25px;
            font-weight: 800;
            font-family: f5f487082c474e4472d76201c069f2098, serif;
            color: #000;
          }

          img {
            width: 80%;
            height: auto;
          }
        }
      }

      @media (max-width: 990px) {
        .submit {
          width: 100px !important;
          height: 30px !important;
          line-height: 30px !important;
        }
      }

      .submit {
        margin-top: 20px;
        float: right;
        width: 146px;
        height: 48px;
        text-align: center;
        line-height: 48px;
        font-size: 16px;
        cursor: pointer;
        user-select: none;
        background: linear-gradient(to right, #03a9f4, #f441a5, #ffeb3b, #09a8f4);
        background-size: 400%;
        border-radius: 50px;
        position: relative;

        a {
          color: #fff;
        }

        &:before {
          content: "";
          position: absolute;
          top: -5px;
          left: -5px;
          bottom: -5px;
          right: -5px;
          background: linear-gradient(to right, #03a9f4, #f441a5, #ffeb3b, #09a8f4);
          background-size: 400%;
          border-radius: 50px;
          filter: blur(3px);
          z-index: -1;
        }

        &:hover {
          animation: submit linear 8s infinite;
        }
      }
    }
  }
}

//联系我结束
//尾部开始
.footer {
  width: 100%;
  height: 240px;
  background-color: #000;
  text-align: center;
  padding-top: 38px;

  h1 {
    font-size: 34px;
    color: #fff;
    font-family: f5f487082c474e4472d76201c069f2098, serif;
  }

  ul {
    width: 200px;
    height: 30px;
    margin: 16px auto 0;
    display: flex;
    align-items: center;
    justify-content: space-around;

    li {
      width: 24px;
      height: 24px;
      background: url("https://f.goodq.top/FeiEditor/images/icon/social_icon_24x24.png") no-repeat;

      &:nth-child(1) {
        background-position: 0 -144px;
      }

      &:nth-child(2) {
        background-position: -72px -144px;
      }

      &:nth-child(3) {
        background-position: -96px -144px;
      }

      &:nth-child(4) {
        background-position: -196px -144px;
      }

      &:nth-child(5) {
        background-position: -504px -144px;
      }
    }
  }

  .Line {
    width: 100%;
    height: 1px;
    margin-top: 50px;
    background-color: #1d1d27;
  }

  p {
    color: #999;
    font-size: 14px;
    height: 54px;
    line-height: 54px;
  }
}

//尾部结束
//侧边导航栏开始
.appMain {
  position: relative;
  top: 0;
  left: 0;
}

.appList {
  width: 100%;
  height: 100%;
  background-color: #cc0033;
  position: fixed;
  top: 0;
  left: 100%;
  z-index: 99999;

  .top {
    height: 52px;
    text-align: right;
    line-height: 52px;
    color: #fff;
    padding-right: 25px;
    font-size: 30px;
    font-weight: 800;

    span {
      cursor: pointer;
    }
  }

  ul {
    li {
      width: 100%;
      height: 39px;
      font-size: 16px;
      line-height: 39px;
      text-align: center;

      a {
        color: #fff;
        display: block;
        padding: 5px 15px;
        border-radius: 10px;

        &:hover {
          background-color: rgba(255, 255, 255, .3);
        }
      }
    }
  }
}

//侧边导航栏结束
//回到顶部
.goTop {
  width: 25px;
  height: 25px;
  position: fixed;
  bottom: 25px;
  right: 25px;
  z-index: 999;

  img {
    width: 100%;
    height: 100%;
    cursor: pointer;
  }
}
</style>
