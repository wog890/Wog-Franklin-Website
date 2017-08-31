<template>
	<div>
		<v-layout row><v-flex md12><div class="divider secondary"></div></v-flex></v-layout>
		<v-layout row>
			<v-flex md6><p class="ma-3">&copy 2017</p></v-flex>
			<v-flex md6>
				<div class="mt-2 mr-2" style="float: right;">
					<template v-for="(media, i) in src.socialMedia">
						<a :href="media.link"><img class="ml-2" :src="media.imgSrc.url" style="height: 29px;"></a>
					</template>
				</div>
			</v-flex>
		</v-layout>
	</div>
</template>

<script>
	import MaxFire from '../maxapps/MaxFire.js'

	export default {
		created() {
			MaxFire.get('/footer').then(oSrcs => {
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
				errorMessage: '',
				loading: true,
				src: {}
			}
		}
	}
</script>

<style scoped>
	.divider {
		height: 2px;
	}
</style>