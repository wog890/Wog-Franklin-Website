<template>
	<v-layout>
	    <v-flex md6>
    		<img class="ma-3" :src="src.logo.imgSrc.url" @click="tabChange">
	    </v-flex>
	    <v-flex md6 class="hidden-xs-only">
			<a href="http://maps.google.com/maps?z=16&q=3941+atlanta+hwy.+athens,+ga.+30606" target="_blank">
				<p class="mt-3 mr-3 mb-0 text-xs-right">
					3941 Atlanta Hwy.<br>Athens, Ga. 30606
				</p>
			</a>
			<p class="mr-3 mb-0 text-xs-right">
				(706) 543-7803<br>Sunday: 12pm-6pm<br>Mon-Sat: 9am-9pm<br>{{specialHours}}
			</p>
			<p class="mr-3 text-xs-right" v-if="editable" style="color: #c90e0e">Editer Mode</p>
	    </v-flex>
	    <v-flex md6 class="hidden-sm-and-up text-xs-right">
	    <!-- <v-flex md6 class="text-xs-right"> -->
	    	<v-btn class="ma-4" dark fab small @click="drawerChanged"><v-icon>menu</v-icon></v-btn>
	    </v-flex>
	</v-layout>
</template>

<script>
	import MaxFire from '../maxapps/MaxFire.js'

	export default {
		created() {
			MaxFire.get('/header').then(oSrcs => {
				this.src = oSrcs;
				this.loading = false;
			}).catch(oErr => {
				this.loading = false;
				this.errorMessage = 'Unable to load page';
				console.log(oErr);
			});
		},
		data: function() {
			return {
				drawer: false,
				errorMessage: '',
				loading: true,
				specialHours: "",
				src: {logo: {imgSrc: {img: '', url: ''}}}
			}
		},
		methods: {
			drawerChanged: function() {
				this.drawer = !this.drawer
				this.$emit('drawerChanged', this.drawer);
			},
			tabChange: function() {
				this.$emit('tabChange', {tabIndex: 'admin'});
			}
		},
		props: {
			editable: {
				type: Boolean,
				default: false
			}
		}
	}
</script>

<style scoped>
	
</style>