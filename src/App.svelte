<script>
	let empleados = [];
	let activado = true
	let datosEmpleado = {
		id: null,
		nombre: "",
		correo: "",
	};

	let mostrarEmpleados = () => {
		fetch("http://localhost/empleados/")
			.then((respuesta) => respuesta.json())
			.then((datosRespuesta) => {
				empleados = datosRespuesta;
				datosEmpleado = {
					id: null,
					nombre: "",
					correo: "",
				};
				activado = true
				console.log(empleados);
			})
			.catch(console.log);
	};
	let agregarEmpleado = () => {
		const nuevoEmpleado = {
			id: datosEmpleado.id,
			nombre: datosEmpleado.nombre,
			correo: datosEmpleado.correo,
		};
		fetch("http://localhost/empleados/?insertar=1", {
			method: "POST",
			body: JSON.stringify(nuevoEmpleado),
		})
			.then((respuesta) => respuesta.json())
			.then((datosRespuesta) => {
				console.log(datosRespuesta);
				mostrarEmpleados();
				// empleados = datosRespuesta;
				// datosEmpleado = {
				// 	id: null,
				// 	nombre:"",
				// 	correo: ""
				// }
				//console.log(empleados);
			})
			.catch(console.log);

		//console.log(nuevoEmpleado)
		//alert("Click para insertar los datos del formulario")
	};
	let borrarEmpleado = (id) => {
		fetch("http://localhost/empleados/?borrar=" + id)
			.then((respuesta) => respuesta.json())
			.then((datosRespuesta) => {
				mostrarEmpleados();
			})
			.catch(console.log);
	};

	let editarEmpleado = (empleado) => {
		activado = false
		datosEmpleado = empleado;
	};

	let actualizarEmpleado = () => {
		fetch("http://localhost/empleados/?actualizar=" + datosEmpleado.id, {
			method: "POST",
			body: JSON.stringify(datosEmpleado),
		})
			.then((respuesta) => respuesta.json())
			.then((datosRespuesta) => {
				console.log(datosRespuesta);
				mostrarEmpleados();
				
			})
			.catch(console.log);
	}

	mostrarEmpleados();
</script>

<div class="container">
	<div class="row">
		<div class="col-md-5">
			<div class="card">
				<div class="card-header">Empleados</div>
				<div class="card-body">
					<form>
						<div class="mb-3">
							<label for="" class="form-label">ID</label>
							<input readonly
								bind:value={datosEmpleado.id}
								type="text"
								class="form-control"
								name=""
								id=""
								aria-describedby="helpId"
								placeholder=""
							/>
						</div>
						<div class="mb-3">
							<label for="" class="form-label">Nombre</label>
							<input
								bind:value={datosEmpleado.nombre}
								type="text"
								class="form-control"
								name=""
								id=""
								aria-describedby="helpId"
								placeholder=""
							/>
						</div>
						<div class="mb-3">
							<label for="" class="form-label">Correo</label>
							<input
								bind:value={datosEmpleado.correo}
								type="text"
								class="form-control"
								name=""
								id=""
								aria-describedby="helpId"
								placeholder=""
							/>
						</div>
						<button
							on:click|preventDefault={agregarEmpleado}
							type="button"
							class="btn btn-primary"
							disabled = {!activado}
							>Agregar empleado</button
						>
						|
						<button
						on:click|preventDefault={actualizarEmpleado}
						 type="button"
						 class="btn btn-primary"
						 disabled = {activado}
						>Actualizar</button
						>
						|
						<button
						on:click|preventDefault={mostrarEmpleados}
						 type="button"
						 class="btn btn-danger"
						>Cancelar</button
						>
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
						{#each empleados as empleado}
							<tr class="">
								<td>{empleado.id}</td>
								<td>{empleado.nombre}</td>
								<td>{empleado.correo}</td>
								<td>
									<button
										type="submit"
										class="btn btn-primary"
										on:click={editarEmpleado(empleado)}
										>Editar</button
									>
									|
									<button
										type="submit"
										class="btn btn-danger"
										on:click={borrarEmpleado(empleado.id)}
										>Borrar</button
									>
								</td>
							</tr>
						{/each}
					</tbody>
				</table>
			</div>
		</div>
	</div>
</div>
