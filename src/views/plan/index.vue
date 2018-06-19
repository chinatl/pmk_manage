<template>
	<div class="plan">
		<div class="erp-select-bar space-between padding20">
       		<div class='erp-search-button'>
				<el-input type='text' size='small' placeholder='Placeholder' v-model='value'></el-input>
				<el-button size='mini' type='primary'><i class="el-icon-search"></i></el-button>
			</div>
      		<div>
      			<button class="erp-btn" @click='open_message'>Emitir Aviso</button>
      		</div>
       	</div>
	 	<div class="erp-list" v-loading='loading'>
			<ul class="title">
				<li>Nome da Loja</li>
				<li>Contato</li>
				<li  class="flex5">E-Mail</li>
				<li>Telefone</li>
				<li class="flex2">Acessos</li>
				<li>Faturamento</li>
				<li class='flex3'>{{$t(`table["Operação"]`)}}</li>
			</ul>
			<transition-group name="fade" tag='div'>
				<ul class="content" v-for='(item,index) in tableData' v-bind:key="index">
					<li>{{item.name}}</li>
					<li>{{item.cancat}}</li>
					<li class="flex5">{{item.email}}</li>
					<li>{{item.phone}}</li>
					<li class="flex2">{{item.access}}</li>
					<li>{{item.fa}}</li>
					<li class='flex3'>
						<div class="table-icon">
							<span v-show='!item.status'><svg-icon icon-class='pause' style='font-size:18px;'></svg-icon></span>
							<span v-show='item.status'><svg-icon icon-class='play' style='font-size:18px;'></svg-icon></span>
							<span @click='edit_dialog= true'><i class="el-icon-edit-outline"></i></span>
							<span><svg-icon icon-class='daochu' style='font-size:16px;font-weight:blod'></svg-icon></span>
						</div>
					</li>
				</ul>
			</transition-group>
		</div>
		<el-dialog  :visible.sync="show_message"
			class='layout-message'
		>
		<div slot='title' class="erp-dialog_title">
			Notificar usuário
		</div>
		<div class='layout-message-title'>
			<h3>Título</h3>
			<el-input size='small'></el-input>
		</div>
		<div class='layout-message-title'>
			<h3>Descrição</h3>
			<el-input 
			 size='small'
			 type="textarea"
			 :autosize="{ minRows: 4, maxRows: 8}">
			 </el-input>
		</div>
		<p class='erp-dialog-button'>
			<button class="erp-btn" @click='submit_message'>{{$t('button["Enviar"]')}}</button>
		</p>
		</el-dialog>
 		<el-dialog  :visible.sync="edit_dialog"
		 class='layout-message'
		>
		<div slot='title' class="erp-dialog_title">
			<div class='big_title'>Editar Cliente | </div>
			<div class="sub_title">
				<p>cadodepaulasilva159@gmail.com  - <i><b>Plano Starter</b></i></p>
				<p><span>(xx) xxxx-xxxx</span><span>Data de Pagamento: Dia 05</span></p>
			</div>
		</div>
		<div class='erp-dialog-item no-border'>
			<div>
				<p>
				Nome de Contato
				</p>
				<el-input  size='small' ></el-input>
			</div>
		</div>
		<div class='erp-dialog-item no-border'>
			<div class="width40">
				<p>
				Loja
				</p>
				<el-input size='small'></el-input>
			</div>
			<div class="width40">
				<p>
				CNPJ/CPF
				</p>
				<el-input  size='small'></el-input>
			</div>
		</div>
		<div class='erp-dialog-item no-border'>
			<div>
				<p>
				Razão Social
				</p>
				<el-input size='small'></el-input>
			</div>
		</div>
		<div class='erp-dialog-item no-border'>
			<div class="width40">
				<p>
				Logradouro
				</p>
				<el-input size='small'></el-input>
			</div>
			<div class="width40">
				<p>
				Número
				</p>
				<el-input size='small'></el-input>
			</div>
		</div>
		<div class='erp-dialog-item no-border'>
			<div>
				<p>
				Complemento
				</p>
				<el-input size='small'></el-input>
			</div>
		</div>
		<div class='erp-dialog-item no-border'>
			<div class="width40">
				<p>
				Bairro
				</p>
				<el-input size='small'></el-input>
			</div>
			<div class="width40">
				<p>
				Cidade
				</p>
				<el-input size='small'></el-input>
			</div>
		</div>
		<div class='erp-dialog-item no-border'>
			<div class="width40">
				<p>
				Estado
				</p>
				<el-input size='small'></el-input>
			</div>
		</div>
		<p class='erp-dialog-button'>
			<button class="erp-btn info circle" @click='submit_edit'>{{$t('button["Concluir"]')}}</button>
		</p>
	</el-dialog>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				show_message: false, //弹框
				edit_dialog: false,
				loading: false,
				tableData: [{
					name: 'Pmcell',
					cancat: 'Ricardo de Paula',
					email: 'cadodepaula@...',
					phone: '(xx) xxxx-xxxx',
					access: '0',
					fa: 'R$ 1.200,00',
					status: true
				}, {
					name: 'Pmcell',
					cancat: 'Ricardo de Paula',
					email: 'cadodepaula@...',
					phone: '(xx) xxxx-xxxx',
					access: '0',
					fa: 'R$ 1.200,00'
				}, {
					name: 'Pmcell',
					cancat: 'Ricardo de Paula',
					email: 'cadodepaula@...',
					phone: '(xx) xxxx-xxxx',
					access: '0',
					fa: 'R$ 1.200,00'
				}, {
					name: 'Pmcell',
					cancat: 'Ricardo de Paula',
					email: 'cadodepaula@...',
					phone: '(xx) xxxx-xxxx',
					access: '0',
					fa: 'R$ 1.200,00'
				}, {
					name: 'Pmcell',
					cancat: 'Ricardo de Paula',
					email: 'cadodepaula@...',
					phone: '(xx) xxxx-xxxx',
					access: '0',
					fa: 'R$ 1.200,00'
				}, {
					name: 'Pmcell',
					cancat: 'Ricardo de Paula',
					email: 'cadodepaula@...',
					phone: '(xx) xxxx-xxxx',
					access: '0',
					fa: 'R$ 1.200,00'
				}, ],
			}
		},
		methods: {
			submit_message() {
				this.show_message = false
			},
			submit_edit() {
				this.edit_dialog = false
			},
			open_message() {
				this.show_message = true
			}
		}
	}

</script>

<style rel="stylesheet/scss" lang="scss">
	.layout-message {
		div.el-dialog {
			width: 760px;
		}
		.layout-message-title {
			margin: 10px 0;
			h3 {
				margin-bottom: 6px;
			}
		}
	}

	.padding20 {
		padding: 0px 20px;
		margin-bottom: 20px;
	}

	.plan {
		.erp-dialog_title {
			overflow: hidden;
			display: flex;
			align-items: center;
			.big_title {
				float: left
			}
			.sub_title {
				float: left;
				font-size: 16px;
				line-height: 24px;
				margin-left: 30px;
			}
		}
	}

</style>
