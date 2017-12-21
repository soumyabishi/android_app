<template>
	<f7-page class="custom-page">
		<f7-navbar theme="22232D" no-shadow back-link="Back" sliding>

		</f7-navbar>

		<f7-block inner>



			<div class="preloaderWrapper" v-if="fetchingData">
				<span class="preloader color-red"></span>
			</div>


			<div class="match_block" v-if="!fetchingData">

				<!--{{JSON.stringify($route.query)}}-->

				<!--<li v-for="(value, key) in $route.query" ><b>{{key}}:</b> {{value}}</li>-->



				<h3 class="ibm-type-semibold"> {{$route.query.fname}} & {{$route.query.sname}}</h3>

				<div class="gif-wrapper">

					<div class="gif-container">
						<img class="lazy-img-fadein" v-lazy="gifUrl">
					</div>

					<div class="heart-wrapper">
						<div id="text">{{ matchData.percentage }}%</div>
						<div id="heart"></div>
					</div>
				</div>


				<p class="ibm-type-italic">{{ matchData.result }}</p>




			</div>

		</f7-block>
	</f7-page>
</template>



<script>

    import axios from "axios";
    import Vue from 'vue';
    import VueTimeago from 'vue-timeago';
    Vue.use(VueTimeago, {
        name: 'timeago', // component name, `timeago` by default
        locale: 'en-US',
        locales: {
            // you will need json-loader in webpack 1
            'en-US': require('vue-timeago/locales/en-US.json')
        }
    });

    export default {

        data() {
            return {
                matchData : {},
				tag:'',
				gifUrl:'',
				fetchingData: false


            }
        },

        methods: {

            fetchPercentageMatch() {
                this.fetchingData = true;
                let config = {
                    headers: {
                        "X-Mashape-Key" : "g0ELE0yeYJmshJ9EJ3Ckwq2tq9g9p1nOJuGjsnlfaR5dIiq06e",
                        "Accept": "application/json"
                    }
                }

                axios.get('https://love-calculator.p.mashape.com/getPercentage?fname=' + this.$route.query.fname + '&' +'sname=' + this.$route.query.sname, config)
                    .then(response => {
                        this.matchData = response.data;
                        if(this.matchData.percentage > 50){
                            this.tag = 'yes'
						}
						else{
                            this.tag = 'nope'
						}
                        this.fetchGiphy();
                    }, error => {
                        console.log(error);
                    });

            },

            fetchGiphy(){
                axios.get('http://api.giphy.com/v1/gifs/random?api_key=zQL46E32vHGYleoiL2Gn23XgpU6Y6XZN&tag='+ this.tag +'&rating=r')

                    .then(response => {
                        this.gifUrl = response.data.data.image_original_url;
                        this.fetchingData = false
                    }, error => {
                        console.log(error);
                    });
			}


    },

        mounted() {
            this.fetchPercentageMatch();
            console.log('calling')
        }
    }
</script>

<style lang="scss">


	.layout-dark .page.custom-page, .theme-red .navbar{
		background-color: #22232D;

		.list-block ul:before{
			display: none;
		}
	}

	.preloaderWrapper{
		text-align: center;
	}


	.match_block{
		text-align: center;
		p{
			font-size: 20px;
			font-weight: 400;
		}
		.gif-wrapper{
			position: relative;

			.gif-container{
				img{
					width: 100%;
				}

			}
		}

		h3{
			font-size: 25px;
		}

		.heart-wrapper{
			width: 100px;
			height: 100px;
			margin:  auto;
			margin-top: -21px;
		}


		#text{
			position:absolute;
			z-index:3;
			margin-left: 35px;
			margin-top: 25px;
			color:white;
			font-size: 19px;
			font-weight: 500;
			-webkit-transition: all .2s ease;
			-moz-transition: all .2s ease;
			transition: all .2s ease;
		}
		#heart {
			position:relative;
			width:100px;
			height:100px;
			-webkit-transition: all .2s ease;
			-moz-transition: all .2s ease;
			transition: all .2s ease;
		}

		#heart:before,#heart:after {
			position:absolute;
			content:"";
			left:50px;
			top:0;
			width:50px;
			height:80px;
			background:#f44336;
			-moz-border-radius:50px 50px 0 0;
			border-radius:50px 50px 0 0;
			-webkit-transform:rotate(-45deg);
			-moz-transform:rotate(-45deg);
			-ms-transform:rotate(-45deg);
			-o-transform:rotate(-45deg);
			transform:rotate(-45deg);
			-webkit-transform-origin:0 100%;
			-moz-transform-origin:0 100%;
			-ms-transform-origin:0 100%;
			-o-transform-origin:0 100%;
			transform-origin:0 100%;
		}

		#heart:after {
			left: 0;
			-webkit-transform:rotate(45deg);
			-moz-transform:rotate(45deg);
			-ms-transform:rotate(45deg);
			-o-transform:rotate(45deg);
			transform:rotate(45deg);
			-webkit-transform-origin:100% 100%;
			-moz-transform-origin:100% 100%;
			-ms-transform-origin:100% 100%;
			-o-transform-origin:100% 100%;
			transform-origin:100% 100%;
		}

	}


	// Lazy loading


	@-webkit-keyframes fadeIn {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}
	@keyframes fadeIn {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}
	.lazy-img-fadein[lazy=loaded] {
		-webkit-animation-duration: 1s;
		animation-duration: 1s;
		-webkit-animation-fill-mode: both;
		animation-fill-mode: both;
		-webkit-animation-name: fadeIn;
		animation-name: fadeIn;
	}
	.lazy-img-fadein[lazy=loading] {
		width: 40px!important;
		margin: auto;
	}
	.lazy-img-fadein[lazy-progressive=true] {
		width: 100%!important;
		margin: auto;
	}
	.lazy-img-fadein[lazy=error] {
		border-radius: 2px;
		-webkit-animation-duration: 1s;
		animation-duration: 1s;
		-webkit-animation-fill-mode: both;
		animation-fill-mode: both;
		-webkit-animation-name: fadeIn;
		animation-name: fadeIn;
	}





</style>
