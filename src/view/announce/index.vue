<template>
	<el-card shadow="always" class="blog-announce" :body-style="{padding: '8px'}">
		<div class="blog-announce-box">
			<div class="blog-announce-left">
				<p><svg-icon icon-class="announcement"></svg-icon>
					天哥新博客开张，欢迎大家踊跃投稿！谢谢大家积极参与！！！
				</p>
			</div>
			<div class="blog-announce-right">
				<a v-if="userInfo && userInfo.nickName" href="javascript:void(0)" @click="editArtical" ><svg-icon icon-class="user" style="color: #999;"></svg-icon> 投稿</a>
				<a v-if="!userInfo.nickName" href="javascript:void(0)" @click="login" style="margin-left: 20px"><svg-icon icon-class="login" style="color: #999;"></svg-icon> 登陆</a>
				<el-dropdown v-if="userInfo && userInfo.nickName" class="dropdown-user"
				@command="handleCommand">
				  <span class="el-dropdown-link">
				  	{{userInfo.nickName}}
				  </span>
				  <el-dropdown-menu slot="dropdown">
				    <el-dropdown-item>评论</el-dropdown-item>
				    <el-dropdown-item>收藏</el-dropdown-item>
				    <el-dropdown-item  command="logout">退出</el-dropdown-item>
				  </el-dropdown-menu>
				</el-dropdown>
			</div>
		</div>
	</el-card>
</template>

<script>
	import { checkLoginStatus } from '@/api/login'
	import { mapGetters } from 'vuex'
	export default {
		name: 'Announce',
		computed: {
			...mapGetters([
					'userInfo'
				])
		},
		methods: {
			editArtical() {
				// checkLoginStatus().then(response => {
				// 	this.$router.push({path: "/editArtical"});
				// })
				this.$router.push({path: "/articleEdit"})
			},
			login() {
				this.$store.dispatch("openLoginDialog")
			},
			handleCommand(command) {
				if(command === "logout"){
					this.$store.dispatch("LogOut").then(response => {
						this.$message({
		          message: '退出登陆',
		          type: 'success'
		        })
		        this.$router.push({ path: '/' })
					})
				}
				
			}
		}
	}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
	.blog-announce {
		width: 80%;
		margin: 0 auto;
		.blog-announce-box {
			display: table;
			width: 100%;
			color: #666;
			font-size: 14px;
			.blog-announce-left {
				display: table-cell;
			}
			.blog-announce-right {
				display: table-cell;
				text-align: right;
				.dropdown-user {
					color: #00a67c;
					font-size: 14px;
					margin-left: 10px;
				}
			}
		}
	}
</style>