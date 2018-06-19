<template>
    <div style="overflow:hidden">
    	<div class='setting-item'>
    		<div class="setting-header">
				{{$t(`setting['Lista de Operadores']`)}}
			</div>
			<div class="erp-list" v-loading='loading'>
				<ul class="title">

					<li>{{$t(`table['Lista de Operadores']`)}}</li>
					<li>{{$t(`table['Grupo']`)}}</li>
					<li>{{$t(`table['Acessos']`)}}</li>
					<li>{{$t(`table['Operação']`)}}</li>
				</ul>
				<transition-group name="fade" tag='div'>
					<ul class="content" v-for='(item,index) in list' v-bind:key="index">
						<li>{{item.item1}}</li>
						<li>{{item.item2}}</li>
						<li>{{item.item3}}</li>
						<li>
							<div class="table-icon">
								<span @click='open_add_dialog'><i class='el-icon-edit-outline'></i></span>
								<span @click='$store.commit("TOGGLE_ALL_DEL")'><i class='el-icon-delete'></i></span>
							</div>
						</li>
					</ul>
				</transition-group>
			</div>
			 <p class='erp-dialog-button'>
				<button class="erp-btn info circle" @click='open_add_dialog'>{{$t(`button['Adicionar operador']`)}}</button>
			</p>
    	</div>
    	<div class='setting-item'>
    		<div class="setting-header">
				{{$t(`table['Grupos']`)}}
			</div>
			<div class="erp-list" v-loading='loading'>
				<ul class="title">
					<li>{{$t(`table['Grupo']`)}} </li>
					<li>{{$t(`table['Acessos']`)}}</li>
					<li>{{$t(`table['Operação']`)}}</li>
				</ul>
				<transition-group name="fade" tag='div'>
					<ul class="content" v-for='(item,index) in list2' v-bind:key="index">
						<li>{{item.item1}}</li>
						<li>{{item.item2}}</li>
						<li>
							<div class="table-icon">
								<span  @click='open_edit_dialog'><i class='el-icon-edit-outline'></i></span>
								<span  @click='$store.commit("TOGGLE_ALL_DEL")'><i class='el-icon-delete'></i></span>
							</div>
						</li>
					</ul>
				</transition-group>
			</div>
			 <p class='erp-dialog-button'>
				<button class="erp-btn info circle"  @click='open_edit_dialog'>{{$t(`button['Criar Grupo']`)}}</button>
			</p>
    	</div>
		<el-dialog
			:visible.sync="add_dialog"
			class='small-dialog'
		>
		<div slot='title' class="erp-dialog_title">
			Adicionar Operador
		</div>
		<div class='erp-dialog-item  no-border'>
			<div>
				<p>Grupos</p>
				<el-select placeholder='Selecione' size='small' style='width:100%' v-model='name'>
					<el-option></el-option>
					<el-option></el-option>
				</el-select>
<!--				<el-input type='text' size='small' placeholder='Pesquisar...' v-model='name'></el-input>-->
			</div>	
		</div>
		<div class='erp-dialog-item  no-border'>
			<div>
				<p>Usuário</p>
				<el-input type='text' size='small' v-model='name'></el-input>
			</div>
		</div>
		<div class='erp-dialog-item  no-border'>
			<div>
				<p>Senha</p>
				<el-input type='text' size='small' v-model='name'></el-input>
			</div>
		</div>
		<div class='erp-dialog-item  no-border'>
			<div>
				<p>Confirmar Senha</p>
				<el-input type='text' size='small' v-model='name'></el-input>
			</div>
		</div>
		
		<p class='erp-dialog-button'>
			<button class="erp-btn  size16 info" @click='submit_add'>{{$t('button["Criar Operador"]')}}</button>
		</p>
	</el-dialog>	
		<el-dialog
			:visible.sync="edit_dialog"
			class='small-dialog'
		>
		<div slot='title' class="erp-dialog_title">
			Editar/Criar Grupo
		</div>
		<div class='erp-dialog-item  no-border'>
			<div>
				<p>Nome do Grupo</p>
				<div class='erp-search-button'>
					<el-input type='text' size='small' v-model='valuex'></el-input>
					<el-button size='mini' type='primary'><i class="el-icon-search"></i></el-button>
				</div>
			</div>	
		</div>
		<div class="erp-list" v-loading='loading'>
			<ul class="title">
				<li class="flex3">{{$t(`table['Módulo']`)}}</li>
				<li class="flex5">{{$t(`table['Descrição']`)}}</li>
				<li class="flex3">{{$t(`table['Operação']`)}}</li>
			</ul>
			<transition-group name="fade" tag='div'>
				<ul class="content" v-for='(item,index) in list1' v-bind:key="index">
					<li class="flex3"><span style="width:120px;text-align:center">{{item.item1}}</span></li>
					<li class="flex5"><span style="width:280px;text-align:left">{{item.desc}}</span></li>
					<li class="flex3">
						<div class="table-icon">
							<span><i class='el-icon-edit-outline'></i></span>
							<span><i class='el-icon-search'></i></span>
							<span><i class='el-icon-error'></i></span>
						</div>
					</li>
				</ul>
			</transition-group>
		</div>
		<p class='erp-dialog-button'>
			<button class="erp-btn  size16 info circle" @click='submit_edit'>{{$t('button["Salvar"]')}}</button>
		</p>
	</el-dialog>
	<my-del></my-del>
	</div>
</template>
<script>
	import myDel from '@/components/Del'
	export default {
		components: {
			myDel
		},
		data() {
			return {
				name: '',
				valuex: '',
				loading: false,
				add_dialog: false,
				edit_dialog: false,
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
					desc: 'Conceder acesso ao Dashboard',
				}, {
					item1: 'Estoquista',
					desc: 'Conceder acesso ao Produto e Anúncio',
				}, {
					item1: 'Expedição',
					desc: 'Conceder acesso a Conferência de Estoque',
				}],
				list2: [{
					item1: 'Vendas',
					item2: 'Ver Acessos',
				}, {
					item1: 'Estoquista',
					item2: 'Ver Acessos',
				}, {
					item1: 'Expedição',
					item2: 'Ver Acessos',
				}]
			}
		},
		methods: {
			add() {

			},
			submit() {

			},
			open_add_dialog() {
				this.add_dialog = true
			},
			open_edit_dialog() {
				this.edit_dialog = true
			},
			submit_add() {
				this.add_dialog = false
			},
			submit_edit() {
				this.edit_dialog = false
			}
		}
	}

</script>
<style rel='stylesheet/scss' lang='scss'>
	.setting-item {
		background-color: #fff;
		padding: 10px 30px 10px 30px;
		.setting-header {
			color: #666;
			font-size: 22rem;
			margin-bottom: 18px;
			border-bottom: 2px solid #ccc;
			padding-bottom: 12px;
		}
	}

</style>
