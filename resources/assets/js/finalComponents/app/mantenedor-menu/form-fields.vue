<template>
	<div class="col-sm-6 col-xs-12">
		<label>Menu padre</label>
		<select-list class-name="form-control col-xs-6" :select-value.sync="dataModel.cod_padre" value-key="id" label-key="name" :url="urlMenu" nullable-label="--Este es padre --"></select-list>
	</div>

	<div class="col-sm-6 col-xs-12">
		<label>Título</label>
		<input type="text" class="form-control" v-model="dataModel.titulo" minlength="3" required>
		<input type="hidden" class="form-control" :value="dataModel.titulo" v-model="dataModel.nombre">
	</div>

	<div class="col-sm-6 col-xs-12">
		<label>Font-Awesome - Icono: <i :class="dataModel.iconclass"></i> </label>
		<input type="text" class="form-control" v-model="dataModel.iconclass" minlength="3"> 
	</div>

	<div class="col-sm-6 col-xs-12">
		<label>Url</label> <small>(Opcional)</small>
		<input type="text" class="form-control" v-model="dataModel.url" minlength="3"> 
	</div>

	<div class="col-sm-6 col-xs-12">
		<label>orden</label>
		<input type="number" class="form-control" v-model="dataModel.orden" min="0"> 
	</div>

	<div class="col-sm-6 col-xs-12">
		<label>Rol de acceso</label>
		<select-list class-name="form-control col-xs-6" :select-value.sync="dataModel.cod_rol" value-key="id" label-key="name" :url="urlRoles" :is-required="true"></select-list>
	</div>

	<div class="col-xs-12">
		<div class="content">
			<button v-if="createMode" class="btn btn-success btn-flat" type="submit"><i class="fa fa-save"></i> GUARDAR</button>
			<button v-else class="btn btn-warning btn-flat" type="submit"><i class="fa fa-save"></i> GUARDAR CAMBIOS</button>
			<a v-link="{path: '/menu'}" class="btn btn-default btn-flat"><i class="fa fa-reply"></i> VOLVER</a>
		</div>

	</div>
</template>

<script>

	import selectList from '../../reusable/select-list.vue';
	import {urlMenuList, urlRoles} from '../config';

	export default {
		beforeCompile(){
			if (this.createMode){
				this.dataModel = this.initModel();
			}
		},
		components: {
			'select-list': selectList
		},
		methods: {
			initModel: function(){
				return {
					cod_padre: null,
					cod_rol: null,
					titulo: null,
					nombre: null,
					iconclass: null,
					url: null,
					orden: null
				}
			},
		},
		data (){
			return{
				urlMenu: urlMenuList,
				urlRoles: urlRoles,
			}
		},
		props: {
			createMode: {
				type: Boolean,
				required: false,
				default: true
			},
			dataModel: {
				type: Object,
				required: false,
				default: function(){
					return {
						cod_padre: null,
						cod_rol: null,
						titulo: null,
						nombre: null,
						iconclass: null,
						url: null,
						orden: null
					}
				}
			}
		}
	}
	
</script>
