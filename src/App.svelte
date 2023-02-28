<script>
	let empleados = [];
	let datosEmpleado = {
		id: null,
		nombre: "",
		correo: ""
	}
	fetch('https://reqres.in/api/users/2')
	.then(respuesta => respuesta.json())
	.then((datosRespuesta)=> {
		empleados = datosRespuesta;
		datosEmpleado = {
			id: null,
			nombre:"",
			correo: ""
		}
		console.log(empleados);

	}).catch(console.log)
</script>

<div class="container">
	<div class="row">
		<div class="col-md-5">
			<div class="card">
				<div class="card-header">
					Empleados
				</div>
				<div class="card-body">
					<form>
						<div class="mb-3">
							<label for="" class="form-label">ID</label>
							<input type="text" class="form-control" name="" id="" aria-describedby="helpId"
								placeholder="">
						</div>
						<div class="mb-3">
							<label for="" class="form-label">Nombre</label>
							<input type="text" class="form-control" name="" id="" aria-describedby="helpId"
								placeholder="">
						</div>
						<div class="mb-3">
							<label for="" class="form-label">Correo</label>
							<input type="text" class="form-control" name="" id="" aria-describedby="helpId"
								placeholder="">
						</div>
						<button type="button" class="btn btn-primary">Agregar empleado</button>
						<button type="button" class="btn btn-primary">Actualizar</button>
					</form>
				</div>
			</div>
		</div>

		<div class="col-7">
			<div class="table-responsive">
				<table class="table">
					<thead>
						<tr>
							<th scope="col">ID</th>
							<th scope="col">Nombre</th>
							<th scope="col">Correo</th>
							<th scope="col">Acciones</th>
						</tr>
					</thead>
					<tbody>
						<tr class="">
							<td>9</td>
							<td>Guedys</td>
							<td>angola@gmail.net</td>
							<td> Editar | Borrar </td>
						</tr>
					</tbody>
				</table>
			</div>
		</div>
	</div>
</div>
	