<template>
	<el-dialog
		:visible.sync="$store.state.product.show_edit"
	>
	<div slot='title' class="edit-title">
		<div class="div1">{{$t('product["Title"]')}}</div>
		<div class="div2">{{$t('product["Selecione o marketplace"]')}}:</div>
		<div class="div3">
			<el-select size='small' placeholder="Mercado Livre | MegaHaribal" style='width:240px'v-model="value">
				<el-option value='1' label="Mercado Livre | MegaHaribal"></el-option>
				<el-option value='2' label="B2W"></el-option>
				<el-option value='3' label="Walmart"></el-option>
				<el-option value='4' label="CNOVA"></el-option>
				<el-option value='5' label="Netshoes"></el-option>
				<el-option value='6' label="Kanui"></el-option>
			</el-select>
		</div>
	</div>
	<div class="entrada-con">
		 <div class="menu menu--prospero">
			<ul class="menu__list">
				<li 
					@click='change_nav(1)'
					:class="current === 1 ? 'menu__item menu__item--current' : 'menu__item'" >
					<a class="menu__link" >{{$t('product["Dados Gerais"]')}}</a>
				</li>
				<li 
					@click='change_nav(2)'
					:class="current === 2 ? 'menu__item menu__item--current' : 'menu__item'" >
					<a class="menu__link">{{$t('product["Video e Imagens"]')}}</a>
				</li>
			</ul>
		</div>
		<div v-show='current === 1'>
			<div class='erp-dialog-item  no-border '>
				<div>
					<p>
				{{$t('product["Clonar"]')}}<i class="el-icon-star-on"></i>
					</p>
					<el-input type='text' size='small' placeholder='URL do anúncio Mercado Livre / ID do anúncio Mercado Livre / SKU B2W '></el-input>
				</div>
			</div>
			<div class='erp-dialog-item no-border'>
				<div>
					<p>
					{{$t('product["Titulo"]')}}
					</p>
					<el-input type='texttext' size='small' placeholder='Escova Alisadora Magic Hair'></el-input>
				</div>
			</div>
			<div class='erp-dialog-item'>
				<div class="erp-dialog-head">{{$t('product["Descrição"]')}}</div>
				<div>
					<p>{{$t('input["Marketplace"]')}}</p>
					<el-select size='small' v-model='form.a'>
						<el-option value='1' label='Texto'></el-option>
						<el-option value='2' label='HTML'></el-option>
					</el-select>
				</div>
				<div class="width100" style='padding-right:20px;'>
					<el-input
					  type="textarea"
					  :autosize='true'
					  v-model="textarea3">
					</el-input>
				</div>
			</div>
			<div class='erp-dialog-item no-border'>
				<div class="width30">
					<p>{{$t('product["Garantia"]')}}</p>
					<el-input  size='small'  v-model='Garantia' disabled></el-input>
				</div>
				<div class="width40">
					<p>{{$t('product["Garantia"]')}}</p>
					<div class='erp-search-button'>
						<el-input type='text' size='small' placeholder='Nome / SKU' v-model='Categoria' disabled></el-input>
						<el-button size='mini' type='primary' @click='open_categorias'><i class="el-icon-search"></i></el-button>
					</div>
				</div>
			</div>
			<div class='erp-dialog-item'>
				<div class="erp-dialog-head">{{$t('input["Precificação"]')}}</div>
				<div>
					<p>{{$t('input["Exposição"]')}}</p>
					<el-select v-model='exposicao' size='small'>
						<el-option value='1' label='Clássico'></el-option>
						<el-option value='2' label='Premium'></el-option>
					</el-select>
				</div>
				<div>
					<p>{{$t('input["Custo"]')}}</p>
					<el-input size='small' v-model='custo' disabled></el-input>
				</div>
				<div>
					<p>{{$t('input["Lucratividade"]')}}</p>
					<el-input size='small' v-model='lucrat' disabled></el-input>
				</div>
				<div>
					<p>{{$t('input["Preço de Venda"]')}}</p>
					<el-input size='small' v-model='value'></el-input>
				</div>
			</div>
			<div class='erp-dialog-item  flex-column'>
				<div class="erp-dialog-head">{{$t('input["Frete"]')}}</div>
				<div >
				<el-checkbox v-model="checked1"><span style='margin-left:12px'>{{$t('product["Frete Grátis"]')}}</span></el-checkbox>
				</div>
				<div >
				<el-checkbox v-model="checked"><span style='margin-left:12px'>{{$t('product["Por conta do Cliente"]')}}</span></el-checkbox></div>
			</div>
			<p class='erp-dialog-button'>
				<el-button type='info' round @click='submit'>{{$t('product["Concluir"]')}}</el-button>
			</p>
			<p class='erp-dialog-button'>
				<button @click='tishi1'>提示1</button>
				<button @click='tishi2'>提示2</button>
				<button @click='tishi3'>提示3</button>
				<button @click='tishi4'>提示4</button>
				<button @click='tishi5'>提示5</button>
			</p>
		</div>
		<div v-show='current === 2'>
			<div class='erp-dialog-item no-border'>
				<div>
					<p>{{$t('product["Produtos"]')}}</p>
					<el-select v-model='select' style='width:400px' size='medium'>
						<el-option value='1' label='Originais do anúncio'></el-option>
						<el-option value='2' label='Minha imagens'></el-option>
					</el-select>
				</div>
			</div>
			<div class="edit-upload">
				<div class="img-src">
					<div class="edit-img-box"  v-show='img_src'>
						<img :src="img_src" alt="" class="edit-img">
					</div>
					<div class="text-edit" v-show='!img_src'>
						<svg-icon icon-class='xiangji' style='font-size:120px'></svg-icon>
						<p>{{$t('product["Adicionar Foto"]')}}</p>
						<p>{{$t('product["Principal"]')}}</p>
					</div>
				</div>
				<el-upload
				  class="upload-demo"
				  drag
				  action="https://jsonplaceholder.typicode.com/posts/"
				  :show-file-list='false'
				  :auto-upload='false'
				  :on-change='changeImg'
				  :file-list="fileList"
				  multiple>
				  <i class="el-icon-upload"></i>
				  <div class="el-upload__text">{{$t('product["Principal"]')}}Arraste e solte sua imagem aqui ou c lique nesta área</div>
				</el-upload>
			</div>
			<nav class="menu menu--ceres img_nav">
				<ul class="menu__list">
					<li :class="img_current === index ? 'menu__item menu__item--current' : 'menu__item' "
					@click='check_img_nav(index)'
					 v-for='(item,index) in nav_data'>
						<a class="menu__link">{{item.title}}</a>
					</li>
				</ul>
			</nav>
			<div class="edit-nav">
				<ul class="block-img">
					<li v-for='(item,index) in nav_data[img_current].list' @mouseenter='mouseenter(item.url)'>
						<img :src="item.url" alt="" class="item-img">
						<i class="el-icon-close" @click='del(index)'></i>
					</li>
				</ul>
			</div>
			<div class="erp-dialog-item">
				<div class="erp-dialog-head">{{$t('product["Descrição"]')}}</div>
				<div>
					<p>{{$t('product["Adicionar URL do Youtube"]')}}</p>
					<el-input  v-model='form.a'  size='small'></el-input>
				</div>
			</div>
			<p class='erp-dialog-button'>
				<el-button type='info' round @click='submit'>{{$t('product["Concluir"]')}}</el-button>
			</p>
		</div>
	</div>
	<el-dialog
		class='edit-Categorias'
		:visible.sync="innerVisible"
		append-to-body>
		<div slot='title' class="erp-dialog_title">
			Categorias
		</div>
		<div class="Categorias-content">
			<div>
				<p>Acessórios para veiculos</p>
				<p>Agro, Industria e Comercio</p>
				<p>Animais</p>
				<p>Antiguidades</p>
				<p>Antiguidades</p>
				<p>Antiguidades</p>
				<p>Antiguidades</p>
				<p>Antiguidades</p>
				<p>Antiguidades</p>
			</div>
			<div>
				<p>Acessórios para veiculos</p>
				<p>Agro, Industria e Comercio</p>
				<p>Animais</p>
				<p>Antiguidades</p>
			</div>
			<div>
				<p>Acessórios para veiculos</p>
				<p>Agro, Industria e Comercio</p>
				<p>Animais</p>
				<p>Antiguidades</p>
			</div>
			<div>
				<p>Acessórios para veiculos</p>
				<p>Agro, Industria e Comercio</p>
				<p>Animais</p>
				<p>Antiguidades</p>
			</div>
			<div>
				<p>Acessórios para veiculos</p>
				<p>Agro, Industria e Comercio</p>
				<p>Animais</p>
				<p>Antiguidades</p>
			</div>
		</div>
		<p class='erp-dialog-button'>
			<button class="erp-btn status" @click='close_categorias'>{{$t('fornecedor["Salvar"]')}}</button>
		</p>
	</el-dialog>
	<my-error 
		:title='title'
		:message='message'
	></my-error>
</el-dialog>
</template>

<script>
	//	import myInput from '@/components/common/input'
	import myError from '@/components/error'
	export default {
		components: {
			myError
		},
		data() {
			return {
				title: 'error',
				message: '',
				innerVisible: false,
				exposicao: '',
				custo: 'R$ 22,00',
				lucrat: 'R$ 120,00',
				img_current: 0,
				current: 1,
				nav_data: [{
					title: this.$t('product["Principal"]'),
					list: []
				}, {
					title: this.$t('product["Preto"]'),
					list: []
				}, {
					title: this.$t('product["Branco"]'),
					list: []
				}, {
					title: this.$t('product["Vermelho"]'),
					list: []
				}, {
					title: this.$t('product["Azul"]'),
					list: []
				}, ],
				fileList: [],
				img_list: [],
				img_src: '',
				select: '2',
				checked: false,
				checked1: false,
				Garantia: '3 Meses',
				Categoria: 'Acessórios / GPS / Aparelhos / Outros',
				value: '',
				textarea3: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed dui mi, gravida molestie convallis sed, sollicitudin in magna. Aliquam erat volutpat. Aliquam erat volutpat. Morbi porttitor, turpis vitae semper interdum, augue mi euismod mauris, a finibus ipsum nunc gravida lectus. Vestibulum sit amet lectus tristique, blandit tellus ac, tempus purus. Quisque suscipit dapibus ligula, nec rhoncus velit congue id. Nullam in tortor turpis. Donec nec convallis elit, id vulputate justo. Fusce eu tortor tristique, laoreet nisi quis, laoreet odio. Suspendisse potenti. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Sed ultricies augue felis, ac cursus neque faucibus bibendum. Integer quis nibh lobortis, tempor elit sit amet, faucibus neque. Vivamus tincidunt quam ante, sit amet iaculis massa molestie vel.",
				user: '',
				form: {
					a: '1',
					Custo: 'R$ 22,00',
					Lucratividade: 'R$ 120,00',
				},
				email: 'cadodepaulasilva159@gmail.com',
				phone: '(xx) xxxxxxxxx',
				tableData: [{
					name: '1000103-00',
					address: 'Escova Alisadora',
					Marca: 'Pmcell',
					Estoque: '200',
					sss: '',
				}, {
					name: '1000103-00',
					address: 'Escova Alisadora',
					Marca: 'Pmcell',
					Estoque: '200',
					sss: '',
				}, {
					name: '1000103-00',
					address: 'Escova Alisadora',
					Marca: 'Pmcell',
					Estoque: '200',
					sss: '',
				}, ]

			}
		},
		methods: {
			tishi1() {
				this.title = 'Atenção!';
				this.message = 'Para anúncios já catalogados na B2W só será possível fazer alterações nos campos de preço e estoque  '
				this.$store.commit("TOGGLE_ALL_ARROR");
			},
			tishi2() {
				this.title = 'Erro de Integração Marketplace!';
				this.message = 'A ação não foi permitida pelo marketplace '
				this.$store.commit("TOGGLE_ALL_ARROR");
			},
			tishi3() {
				this.title = 'Error!';
				this.message = ['Ocorreu um erro!', 'Favor entrar em contato com a equipe Hariexpress.']
				this.$store.commit("TOGGLE_ALL_ARROR");
			},
			tishi4() {
				this.title = 'Informação!';
				this.message = 'Favor verificar se todos os campos foram preenchidos corretamente.'
				this.$store.commit("TOGGLE_ALL_ARROR");
			},
			tishi5() {
				this.title = 'Informação!';
				this.message = 'Ação realizada com sucesso!'
				this.$store.commit("TOGGLE_ALL_ARROR");
			},
			close_categorias() {
				this.innerVisible = false
			},
			open_categorias() {
				this.innerVisible = true;
				console.log(1)
				this.$get('https://api.mercadolibre.com/sites/MLB/categories').then(res => {
					console.log(res)
				})
			},
			change_nav(current) {
				//				this.current = 0;
				this.current = current;
			},
			mouseenter(src) {
				this.img_src = src;
			},
			submit() {
				this.$message({
					message: '恭喜你，操作成功',
					type: 'success'
				});
			},
			check_img_nav(index) {
				this.img_current = index;
				if (!this.nav_data[index].list.length) {
					this.img_src = ''
				} else {
					this.img_src = this.nav_data[this.img_current].list[0].url
				}
			},
			changeImg(e, i) {
				this.img_src = e.url;
				this.nav_data[this.img_current].list.push(e);
			},
			del(index) {
				this.nav_data[this.img_current].list.splice(index, 1);
				if (this.nav_data[this.img_current].list.length === 0) {
					this.img_src = ''
				}
			}
		},
		created() {

		}
	}

</script>
<style rel="stylesheet/scss" lang="scss">
	$fs20:18rem;
	.el-dialog {
		margin-bottom: 20px
	}

	.edit-upload {
		height: 240px;
		position: relative;
		.img-src {
			height: 100%;
			width: 320px;
			float: left;
			background-color: #e8e8e8;
			display: flex;
			align-items: center;
			justify-content: center;
			align-items: center;
			position: absolute;
			top: 0;
			left: 0;
			flex-flow: wrap;
			.edit-img-box {
				width: 100%;
				height: 100%;
				display: flex;
				align-items: center;
				justify-content: center;
				background-color: #fff
			}
			.edit-img {
				max-height: 100%;
				max-width: 100%;

			}
			.text-edit {
				p {
					text-align: center;
					margin: 0;
					padding: 0;
					height: 16px;
					font-weight: bold;
				}
			}
		}
		.upload-demo {
			width: 100%;
			padding-left: 370px;
			float: left;
			height: 100%;
			.el-upload {
				width: 100%;
				height: 100%;
				.el-upload-dragger {
					width: 100%;
					height: 100%;
				}
			}
		}
	}

	.img_nav {}

	.edit-nav {
		margin-bottom: 40px;
		font-size: 18rem;
		.block-img {
			overflow: hidden;
			margin-top: 20px;
			width: 100%;
			li {
				width: 100px;
				height: 100px;
				float: left;
				margin-right: 20px;
				display: flex;
				justify-content: center;
				align-items: center;
				/*				border: 1px solid #ccc;*/
				position: relative;
				.item-img {
					max-width: 100%;
					max-height: 100%
				}
				.el-icon-close {
					position: absolute;
					right: 0;
					top: 0;
					cursor: pointer;
				}
			}
		}
	}

	.edit-title {
		padding: 15px 0;
		margin: 0 30px;
		border-bottom: 2px solid #ccc;
		display: flex;
		align-items: center;
		.div1 {
			font-size: 30rem;
			margin-right: 30px;
		}
		.div2 {
			font-size: 15rem;
			margin-right: 30px;
		}

	}

	.entrada-con {
		.edit-form {
			margin-top: 20px;
			.label {
				font-size: 20rem;
				margin-bottom: 8px;
				.el-icon-star-on {
					color: #E2B04D;
					margin-left: 12px;
				}
			}
		}
		.edit-abled {
			display: flex;
			justify-content: space-between;
		}
		.el-table--enable-row-transition .el-table__body td {
			padding: 0
		}
		.part2 {
			margin-top: 20px;
			.span {
				margin-right: 20px;
				font-size: 14px;
				font-weight: bold
			}
		}
		padding: 10px 30px;
		.entrada-h3 {
			text-align: center;
			display: flex;
			justify-content: center;
			align-items: center;
			height: 40px;
			line-height: 40px;
			.item {
				width: 50%;
				font-size: 18px;
				color: #000;
				cursor: pointer;
				span {
					border-radius: 50%;
					font-size: 14px;
					background-color: #ccc;
					padding: 4px;
					display: inline-block;
					width: 20px;
					height: 20px;
					line-height: 12px;
					margin-right: 4px;
					position: relative;
					top: -2px;
					color: #fff
				}
			}
			>.current {
				background-color: #eee;
			}
		}

		.edit-item {
			border: 2px solid #eee;
			border-radius: 5px;
			padding: 30px;
			position: relative;
			margin-top: 30px;
			display: flex;
			justify-content: space-between;
			flex-flow: wrap;
			.edit-input-item {
				width: 100%;
				margin-bottom: 20px;
				margin-right: 20px;
				.label {
					margin: 8px 0;
					font-size: $fs20;
					font-weight: normal;
					color: #666
				}
				.edit-textarea {
					width: 100%;
					margin-top: 20px;
				}
			}
			.entrada-item-title {
				position: absolute;
				top: -22px;
				left: 100px;
				padding: 10px 20px;
				height: 30px;
				background-color: #fff;
				font-size: 20rem;
			}
			.entrada-input-item1 {
				width: 20%;
				margin-bottom: 20px;
				margin-right: 20px;
				.label {
					margin: 8px 0;
					font-size: $fs20;
					font-weight: normal;
					color: #666
				}
			}
			.entrada-input-item {
				width: 22%;
				margin-bottom: 20px;
				.label {
					margin: 8px 0;
					font-size: $fs20;
					font-weight: normal;
					color: #666
				}
			}
		}
		.edit-item1 {
			border: 2px solid #eee;
			border-radius: 5px;
			padding: 30px;
			position: relative;
			margin-top: 30px;
			margin-bottom: 30px;
			display: flex;
			.entrada-item-title {
				position: absolute;
				top: -22px;
				left: 100px;
				padding: 10px 20px;
				height: 30px;
				background-color: #fff;
				font-size: 20rem;
			}
			.entrada-input-item1 {
				width: 28%;
				margin-right: 60px;
				.label {
					margin: 8px 0;
					font-size: $fs20;
					font-weight: normal;
					color: #666
				}

			}
		}
		.entrada-btn {
			text-align: right;
			.span {
				font-size: 16px;
				padding: 0 6px;

			}
		}

	}

	.el-dialog__body {
		padding: 10px 20px;
	}

	.edit-Categorias {
		.el-dialog {
			background-color: #f5f5f6;
		}
		.Categorias-content {
			display: flex;
			align-items: flex-start;
			justify-content: space-between;
			div {
				width: 18%;
				padding: 8px 12px;
				background-color: #fff;
			}
		}
	}

</style>
