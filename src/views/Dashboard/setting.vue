<template>
	<div style="overflow:hidden">
		<div class="operadores-item">
			<div class="setting-header">
				{{$t(`setting['Senha']`)}}
			</div>
			<div class="setting-content">
				<div class="setting-content-input">
					<span class='name '>{{$t(`setting['Senha de Login']`)}}:</span>
					<el-input size='small' type='password' style='width:50%'></el-input>
				<i class='el-icon-edit-outline' @click='$store.commit("TOOGLE_EDIT_PWD")'></i>
				</div>
				<div class="setting-content-input">
					<span class='name'>{{$t(`setting['Telefone']`)}}:</span>
					<el-input size='small' value='xxxxxxxx' style='width:50%'></el-input>
					<i class='el-icon-edit-outline'
				@click='$store.commit("TOOGLE_EDIT_PHONE")'	
					></i>
				</div>
				<div class="setting-content-input">
					<span class='name'>{{$t(`setting['Senha de Administração']`)}}:</span>
					<el-input size='small' type='password' style='width:50%'></el-input>
					<i class='el-icon-edit-outline'
					@click='$store.commit("TOOGLE_EDIT_TRADE")'
					></i>
				</div>
			</div>
		</div>
		<div class="operadores-item">
			<div class="setting-header">
				{{$t(`setting['Taxa de Comissão']`)}}
			</div>
			<div class="setting-item">
				<div>
					<!-- class="filter-gray"-->
					<h6>Mercado Livre</h6>
					<div class="setting-item-img">
						<img :src="require('@/assets/market/market-liver.png')" alt="">
					</div>
					<p class="setting-item-tip">
						<span>{{$t(`setting['Clássico']`)}}</span>
						<span>{{$t(`setting['Premium']`)}}</span>
					</p>
					<div class="setting-item-footer">
						<div class='setting-search-button'>
							<el-input type='text' size='small' v-model='value'></el-input>
							<el-input type='text' size='small' v-model='value1'></el-input>
							<el-button size='mini' type='primary'><i class="el-icon-check"></i></el-button>
						</div>
					</div>
				</div>
				<div>
					<!-- class="filter-gray"-->
					<h6>B2W</h6>
					<div class="setting-item-img">
						<img :src="require('@/assets/market/market-b2w.png')" alt="">
					</div>
					<p class="setting-item-tip">
						<span>{{$t(`setting['Comissão Mkt']`)}}.</span>
					</p>
					<div class="setting-item-footer">
						<div class='erp-search-button'>
							<el-input type='text' size='small' placeholder='Nome / SKU' v-model='b2w'></el-input>
							<el-button size='small' type='primary'>ok</el-button>
						</div>
					</div>
				</div>
				<div>
					<!-- class="filter-gray"-->
					<h6>{{$t(`setting['Comissão Mkt']`)}}..</h6>
					<div class="setting-item-img">
						<img :src="require('@/assets/market/wmarket-woerma.png')" alt="">
					</div>
					<p class="setting-item-tip">
						<span>{{$t(`setting['Comissão Mkt']`)}}..</span>
					</p>
					<div class="setting-item-footer">
						<div class='erp-search-button'>
							<el-input type='text' size='small' placeholder='Nome / SKU' v-model='walmart'></el-input>
							<el-button size='small' type='primary'>ok</el-button>
						</div>
					</div>
				</div>
			</div>
		</div>
		<edit-password></edit-password>
		<edit-phone></edit-phone>
		<edit-trade></edit-trade>
	</div>

</template>
<script>
	import editPassword from './components/edit_pwd.vue';
	import editPhone from './components/edit_phone.vue'
	import editTrade from './components/edit_trade.vue'
	export default {
		components: {
			editPassword,
			editTrade,
			editPhone
		},
		data() {
			return {
				loading: false,
				value: '11%',
				value1: '16%',
				b2w: '16%',
				walmart: '16%',
				list: [{
					item1: 'Ricardo',
					item2: 'Vendas',
					item3: 'Ver Acessos',
				}, {
					item1: 'Rodrigo',
					item2: 'Estoquista',
					item3: 'Ver Acessos',
				}, {
					item1: 'Pedro',
					item2: 'Expedição',
					item3: 'Ver Acessos',
				}],
				list1: [{
					item1: 'Vendas',
					item2: 'Ver Acessos',
				}, {
					item1: 'Estoquista',
					item2: 'Ver Acessos',
				}, {
					item1: 'Expedição',
					item2: 'Ver Acessos',
				}, ]
			}
		},
		methods: {
			add() {

			}
		}
	}

</script>
<style rel='stylesheet/scss' lang='scss'>
	.operadores-item {
		background-color: #fff;
		padding: 30px 30px;
		margin-bottom: 30px;
		.setting-header {
			color: #999;
			font-size: 24rem;
			margin-bottom: 12px;
		}
		.setting-content {
			padding-left: 6px;
			.setting-content-input {
				display: flex;
				margin: 14px 0;
				align-items: center;
				.name {
					width: 240px;
					font-size: 16rem;
					display: inline-block;
					color: #999;
					margin-right: 20px;
				}
				i {
					font-size: 24px;
					margin-left: 12px;
					color: #999;
					font-weight: normal;
					cursor: pointer;
				}
			}
		}
		.setting-item {
			display: flex;
			padding-left: 6px;
			>div {
				width: 240px;
				min-width: 240px;
				border: 1px solid #ccc;
				border-radius: 16px;
				overflow: hidden;
				margin-right: 40px;
				margin-top: 10px;
				padding: 20px;
				h6 {
					text-align: center;
					font-size: 18px;
					height: 40px;
					line-height: 40px
				}
				.setting-item-img {
					height: 100px;
					display: flex;
					justify-content: center;
					align-items: center;
					img {
						/*					width: 100px;*/
					}
				}
				.setting-item-tip {
					text-align: left;
					margin-bottom: 6px;
					height: 40px;
					line-height: 40px;
					font-size: 16rem;
					color: #000;
					span {
						padding-left: 6px;
						border-left: 2px solid #999;
						margin-right: 12px;
					}
				}
				.setting-item-footer {
					.el-input__inner {
						padding: 0 6px;
					}
					.setting-search-button {
						display: flex;
						justify-content: center;
						align-items: center;
						.el-button--mini {
							padding: 7px;
							border-radius: 0 4px 4px 0;
						}
						.el-input__inner {
							border-radius: 4px 0 0 4px;
						}
						i {
							font-size: 16px;
						}
						.el-button--small {
							padding: 8px;
							border-radius: 0 4px 4px 0;
							span {
								font-size: 14px;
							}
						}
					}
				}

			}
		}
	}

</style>
