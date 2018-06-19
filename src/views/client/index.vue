<template>
<div>
	<div class="list-item">
		<ul>
			<li v-for="(element,index) in myArray" :key="element.id"  draggable="true" @dragstart='dragstart(index)'>
				{{element.name}}
			</li>
		</ul>
	</div>
	<div class="client-c">
		<div class="client-list">
			<h3>
				<span class="title">Plano Starter</span>
				<el-input size='small' style='width:90px' v-model='form_level1.monthPricer' @keyup.native.enter ='updaye_price("1",$event)'>
					<i slot="prefix" class="fs" style="color:#666">R$</i>
				</el-input>
			</h3>
			<div class="client-con" v-loading='form_loading1'>
				<ul @drop='drop("1")' @dragover="allowDrop">
					<li v-for='(item,i) in list1' draggable="true" @dragstart='dragstartList' @dragend='isDragover($event,i,list1,"1")'>
						<span>{{item.name}}</span>
						<span><el-input size='small' style='width:80px' v-model='form_level1[item.label]' v-show=' item.id != 41 && item.id != 61 '
						 @keyup.native.enter ='updaye_price("1",$event)'>
						 	<i slot="prefix" class="el-input__icon" style="color:#666" v-if='item.id == 81 || item.id == 91'>R$</i>
						 </el-input></span>
					</li>
				</ul>
			</div>
		</div>
		<div class="client-list">
			<h3>
				<span class="title">Plano Premium</span>
				<el-input size='small' style='width:90px'v-model='form_level2.monthPricer' @keyup.native.enter ='updaye_price("1",$event)'>
					<i slot="prefix" class="fs" style="color:#666">R$</i>
				</el-input>
			</h3>
			<div class="client-con" v-loading='form_loading2'>
				<ul @drop='drop("2")' @dragover="allowDrop">
					<li v-for='(item,i) in list2' draggable="true" @dragstart='dragstartList' @dragend='isDragover($event,i,list2,"2")'>
						<span>{{item.name}}</span>
						<span><el-input size='small' style='width:80px' v-model='form_level2[item.label]' 
					 	@keyup.native.enter ='updaye_price("1",$event)'
						v-show=' item.id != 41 && item.id != 61 '>
							<i slot="prefix" class="el-input__icon" style="color:#666" v-if='item.id == 81 || item.id == 91'>R$</i>
						</el-input></span>
					</li>
				</ul>
			</div>
		</div>
		<div class="client-list">
			<h3>
				<span class="title">Plano VIP</span>
				<el-input size='small' style='width:90px' v-model='form_level3.monthPricer' @keyup.native.enter ='updaye_price("1",$event)'>
					<i slot="prefix" class="fs" style="color:#666">R$</i>
				</el-input>
			</h3>
			<div class="client-con" v-loading='form_loading3'>
				<ul @drop='drop("3")' @dragover="allowDrop">
					<li v-for='(item,i) in list3' draggable="true" @dragstart='dragstartList' @dragend='isDragover($event,i,list3,"3")'>
						<span>{{item.name}}</span>
						<span><el-input size='small' style='width:80px' v-model='form_level3[item.label]' 
						@keyup.native.enter ='updaye_price("1",$event)'
						v-show=' item.id != 41 && item.id != 61 '>
							<i slot="prefix" class="el-input__icon" style="color:#666" v-if='item.id == 81 || item.id == 91'>R$</i>
						</el-input></span>
					</li>
				</ul>
			</div>
		</div>
	</div>
</div>

</template>
<script>
	import {
		validataNum
	} from '@/utils/validate'
	export default {
		name: 'dragKanban-demo',
		data() {
			return {
				myArray: [{
					name: "Mercado Livre",
					id: 11,
					label: 'mercadoLivreNumber',
				}, {
					name: "B2W",
					id: 21,
					label: 'b2wNumber'
				}, {
					name: "Walmart",
					id: 31,
					label: 'walmartNumber'
				}, {
					name: "Precificação B2W",
					id: 41,
					label: 'b2wBuyBox'
				}, {
					name: "Clonar Loja",
					id: 51,
					label: 'cloneNumber'
				}, {
					name: "Anúncio BuyBox",
					id: 61,
					label: 'mercadoLivreBuyBox'
				}, {
					name: "Compartilhar no Facebook",
					id: 71,
					label: 'facebookShareNumber'
				}, {
					name: "Desconto Semestral",
					id: 81,
					label: 'halfPricer'
				}, {
					name: "Desconto Anual",
					id: 91,
					label: 'yearPricer'
				}],
				list1: [],
				list2: [],
				list3: [],
				index: null,
				flag: true,
				pageX: 0,
				pageY: 0,
				form_level1: {
					"b2wBuyBox": "",
					"b2wNumber": '',
					"cloneNumber": '',
					"createID": "123456",
					"facebookShareNumber": '',
					"halfPricer": '',
					"level": "1",
					"mercadoLivreBuyBox": '',
					"mercadoLivreNumber": '',
					"monthPricer": '',
					"packageId": "",
					"updateDate": "",
					"walmartNumber": '',
					"yearPricer": '',
					"type": 'add'
				},
				form_level2: {
					"b2wBuyBox": "",
					"b2wNumber": '',
					"cloneNumber": '',
					"createID": "123456",
					"facebookShareNumber": '',
					"halfPricer": '',
					"level": "2",
					"mercadoLivreBuyBox": '',
					"mercadoLivreNumber": '',
					"monthPricer": '',
					"packageId": "",
					"updateDate": "",
					"walmartNumber": '',
					"yearPricer": '',
					"type": 'add'
				},
				form_level3: {
					"b2wBuyBox": "",
					"b2wNumber": '',
					"cloneNumber": '',
					"createID": "123456",
					"facebookShareNumber": '',
					"halfPricer": '',
					"level": "3",
					"mercadoLivreBuyBox": '',
					"mercadoLivreNumber": '',
					"monthPricer": '',
					"packageId": "",
					"updateDate": "",
					"walmartNumber": '',
					"yearPricer": '',
					"type": 'add'
				},
				updateID: '123456',
				form_loading1: false,
				form_loading2: false,
				form_loading3: false,
			}
		},
		created() {
			this.init(0);
		},
		methods: {
			init(index) {
				if (index === 0) {
					this.form_loading1 = true;
					this.form_loading2 = true;
					this.form_loading3 = true;
				} else {
					this['form_loading' + index] = true;
				}
				this.$get('sys/package/list').then(res => {
					for (var i = 0; i < res.data.length; i++) {
						this.form_loading1 = false;
						this.form_loading2 = false;
						this.form_loading3 = false;
						if (res.data[i].level === '0') {
							this.form_level1.type = 'update';
							this.form_level1 = res.data[i];
							this.list1 = this.getInitList(res.data[i]);
						} else if (res.data[i].level === '1') {
							this.form_level2.type = 'update';
							this.form_level2 = res.data[i];
							this.list2 = this.getInitList(res.data[i]);
						} else if (res.data[i].level === '2') {
							this.form_level3.type = 'update';
							this.form_level3 = res.data[i];
							this.list3 = this.getInitList(res.data[i]);
						}
					}
				})
			},
			updaye_price(name, e) {
				if (!e.target.value) {
					return
				}
				if (!validataNum(e.target.value)) {
					this.$message({
						message: '你输入格式有误',
						type: 'error'
					})
					return
				}
				var form = this['form_level' + name];
				this['form_loading' + name] = true;
				this.$post('sys/package/update', {
					"b2wNumber": form.b2wNumber,
					"b2wBuyBox": form.b2wBuyBox,
					"cloneNumber": form.cloneNumber,
					"facebookShareNumber": form.facebookShareNumber,
					"halfPricer": form.halfPricer,
					"level": form.level,
					"mercadoLivreBuyBox": form.mercadoLivreBuyBox,
					"mercadoLivreNumber": form.mercadoLivreNumber,
					"monthPricer": form.monthPricer,
					"b2wBuyBox": form.b2wBuyBox,
					"packageId": form.packageId,
					"walmartNumber": form.walmartNumber,
					"yearPricer": form.yearPricer,
					"updateID": this.updateID,
				}).then(res => {
					this['form_loading' + name] = false;
					e.target.blur();
					this.$message({
						message: res.data,
						type: 'success'
					})
				}).catch(res => {
					this['form_loading' + name] = false;
				})
			},
			/*舒适化列表*/
			getInitList(obj) {
				var arr = [];
				for (var i = 0; i < this.myArray.length; i++) {
					for (var k in obj) {
						if (obj[k] != 0) {
							if (k === this.myArray[i].label) {
								arr.push(this.myArray[i])
							}
						}
					}
				}
				return arr.sort(this.compare('id'))
			},
			compare(property) {
				return function(a, b) {
					var value1 = a[property];
					var value2 = b[property];
					return value1 - value2;
				}
			},
			dragstartList(event) {
				this.flag = false
			},
			isDragover(e, index, list, level) {
				var flag = false;
				var form = this['form_level' + level];
				if (e.offsetX < 0) {
					flag = true
				}
				if (e.offsetX - e.target.clientWidth > 0) {
					flag = true
				}
				if (flag) {
					this["form_loading" + level] = true;
					form[list[index]["label"]] = 0;
					this.$post('sys/package/update', {
						"b2wNumber": form.b2wNumber,
						"b2wBuyBox": form.b2wBuyBox,
						"cloneNumber": form.cloneNumber,
						"facebookShareNumber": form.facebookShareNumber,
						"halfPricer": form.halfPricer,
						"level": form.level,
						"mercadoLivreBuyBox": form.mercadoLivreBuyBox,
						"mercadoLivreNumber": form.mercadoLivreNumber,
						"monthPricer": form.monthPricer,
						"b2wBuyBox": form.b2wBuyBox,
						"packageId": form.packageId,
						"walmartNumber": form.walmartNumber,
						"yearPricer": form.yearPricer,
						"updateID": this.updateID
					}).then(res => {
						this["form_loading" + level] = false;
						list.splice(index, 1)
						this.$message({
							message: '删除成功',
							type: 'success'
						})
					}).catch(res => {
						this["form_loading" + level] = false;
					})
				}
			},
			dragstart(index) {
				this.flag = true;
				this.index = index;
			},
			allowDrop(e) {
				e.preventDefault();
			},
			checkSame(arr, index) {
				for (var i = 0; i < arr.length; i++) {
					if (arr[i].name === this.myArray[this.index].name) {
						return true
					}
				}
				return false
			},
			drop(index) {
				var list = this['list' + index];
				var form = this['form_level' + index]
				if (!this.flag) {
					return
				}
				if (this.checkSame(list)) {
					this.$message({
						message: '已经添加过相同的元素',
						type: 'error'
					});
					return
				}
				this['form_loading' + index] = true;
				var label = this.myArray[this.index].label;
				if (this.form_level1.type === 'add') {
					this.$post('sys/package/save', {
						"updateID": this.updateID,
						label: form[label]
					}).then(res => {
						this['form_loading' + index] = false;
						form.type === 'update';
						list.push(this.myArray[this.index]);
						list.sort(this.compare('id'))
						this.init();
					}).catch(res => {
						this['form_loading' + index] = false;
					})
				} else {
					if (this.myArray[this.index].id === 61 || this.myArray[this.index].id === 41) {
						form[label] = '1'
					}
					this.$post('sys/package/update', {
						"b2wNumber": form.b2wNumber,
						"b2wBuyBox": form.b2wBuyBox,
						"cloneNumber": form.cloneNumber,
						"facebookShareNumber": form.facebookShareNumber,
						"halfPricer": form.halfPricer,
						"level": form.level,
						"mercadoLivreBuyBox": form.mercadoLivreBuyBox,
						"mercadoLivreNumber": form.mercadoLivreNumber,
						"monthPricer": form.monthPricer,
						"b2wBuyBox": form.b2wBuyBox,
						"packageId": form.packageId,
						"walmartNumber": form.walmartNumber,
						"yearPricer": form.yearPricer,
						"updateID": this.updateID
					}).then(res => {
						this['form_loading' + index] = false;
						list.push(this.myArray[this.index]);
						list.sort(this.compare('id'))
						this.$message({
							message: '新增一个标签成功',
							type: 'success'
						})
					}).catch(res => {
						this['form_loading' + index] = false;
					})
				}
			}
		}
	}

</script>
<style lang="scss">
	.list-item {
		background-color: #fff;
		padding: 12px;
		margin-bottom: 20px;
		ul {
			overflow: hidden;
			li {
				width: 200px;
				height: 60px;
				line-height: 18px;
				text-align: center;
				background-color: #f5f5f6;
				font-size: 16px;
				font-weight: bold;
				padding: 0px 20px;
				color: #666;
				float: left;
				margin: 15px;
				display: flex;
				align-items: center;
				justify-content: center;
				cursor: pointer;
				&:hover {
					background-color: #eaedf3;
				}
			}
		}
	}

	.client-c {
		padding: 27px;
		background-color: #fff;
		overflow: hidden;
		.client-list {
			float: left;
			margin-right: 20px;
			width: 300px;
			border-radius: 10px;
			h3 {
				background-color: #00C1DE;
				height: 60px;
				line-height: 60px;
				border-radius: 10px 10px 0 0;
				display: flex;
				padding: 0 20px;
				justify-content: space-between;
				align-items: center;
				.title {
					font-size: 18px;
					color: #fff;
				}
			}
			.client-con {
				border: 2px solid #e8e8e8;
				border-top: none;
				padding: 6px 12px;
				border-radius: 0 0 10px 10px;
				ul {
					height: 546px;
					li {
						background-color: #f5f5f6;
						display: flex;
						justify-content: space-between;
						align-items: center;
						padding: 10px;
						border-radius: 4px;
						margin: 12px 0;
						span {
							font-size: 16px;
						}
					}
				}
			}
		}
	}

</style>
