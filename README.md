<?php 
SESSION_START();
if (isset($_SESSION['usuario'])) {

}
else{
	header("location: login.php");
}
?>


<?php  
//index.php
$connect = mysqli_connect("localhost", "root", "", "pruebadb");
mysqli_set_charset($connect,"utf8");

$query = "SELECT * FROM control  WHERE idr = '".$_GET["idr"]."'";
$result = mysqli_query($connect, $query);

$query = "SELECT * FROM requerimientos  WHERE idreq = '".$_GET["idr"]."'";
$resultado = mysqli_query($connect, $query);

$_SESSION['id'] = $_GET["idr"];
$_SESSION['cr'] = $_GET["idr"];

$query = "SELECT * FROM formulario  WHERE idf = '".$_SESSION['id']."'";
$resultado2 = mysqli_query($connect, $query);

$query = "SELECT * FROM requerimientos  WHERE idreq = '".$_SESSION['id']."'";
$resultado3 = mysqli_query($connect, $query);

$query = "SELECT * FROM seleccion  WHERE ids = '".$_SESSION['id']."'";
$resultado4 = mysqli_query($connect, $query);

$query = "SELECT * FROM seleccion  WHERE ids = '".$_SESSION['id']."'";
$resultado4a = mysqli_query($connect, $query);

$query = "SELECT * FROM requerimientos  WHERE idreq = '".$_SESSION['id']."'";
$resultado5 = mysqli_query($connect, $query);

$query = "SELECT * FROM requerimientos  WHERE idreq = '".$_SESSION['id']."'";
$resultado5a = mysqli_query($connect, $query);

$query = "SELECT * FROM docproveedor  WHERE iddocp = '".$_SESSION['id']."'";
$docproveedor = mysqli_query($connect, $query);

$query = "SELECT * FROM docproveedor  WHERE iddocp = '".$_SESSION['id']."'";
$docproveedora = mysqli_query($connect, $query);

$query = "SELECT * FROM sustentos  WHERE idr = '".$_SESSION['id']."'";
$docsustentos = mysqli_query($connect, $query);

$query = "SELECT * FROM sustentos  WHERE idr = '".$_SESSION['id']."'";
$docsustentosa = mysqli_query($connect, $query);

$query = "SELECT * FROM requerimientos  WHERE idreq = '".$_SESSION['id']."'";
$contrato = mysqli_query($connect, $query);

$query = "SELECT * FROM contratos  WHERE idc = '".$_SESSION['id']."'";
$estado = mysqli_query($connect, $query);


$query = "SELECT * FROM criterios  WHERE idc = '".$_SESSION['id']."'";
$resultadoc = mysqli_query($connect, $query);

$query = "SELECT * FROM criterios  WHERE idc = '".$_SESSION['id']."'";
$resultadocr = mysqli_query($connect, $query);

$query = "SELECT * FROM pcriterios  WHERE idpc = '".$_SESSION['id']."'";
$resultadop = mysqli_query($connect, $query);



$query = "SELECT * FROM criterios  WHERE idc = '".$_SESSION['id']."'";
$resultadocv = mysqli_query($connect, $query);

$query = "SELECT * FROM criterios  WHERE idc = '".$_SESSION['id']."'";
$resultadocrv = mysqli_query($connect, $query);

$query = "SELECT * FROM pcriterios  WHERE idpc = '".$_SESSION['id']."'";
$resultadopv = mysqli_query($connect, $query);

$query = "SELECT * FROM valoracion  WHERE idv = '".$_SESSION['id']."'";
$resultadov = mysqli_query($connect, $query);

$query = "SELECT * FROM criterios  WHERE idc = '".$_SESSION['id']."'";
$resultadocva = mysqli_query($connect, $query);


$query = "SELECT * FROM subtotal  WHERE idr = '".$_SESSION['id']."' and idp = '1'" ;
$resultadost = mysqli_query($connect, $query);

$query = "SELECT * FROM subtotal  WHERE idr = '".$_SESSION['id']."' and idp = '2'" ;
$resultadost1 = mysqli_query($connect, $query);

$query = "SELECT * FROM subtotal  WHERE idr = '".$_SESSION['id']."' and idp = '3'" ;
$resultadost2 = mysqli_query($connect, $query);

$query = "SELECT * FROM subtotal  WHERE idr = '".$_SESSION['id']."' and idp = '4'" ;
$resultadost3 = mysqli_query($connect, $query);

$query = "SELECT * FROM subtotal  WHERE idr = '".$_SESSION['id']."' and idp = '5'" ;
$resultadost4 = mysqli_query($connect, $query);

$query = "SELECT * FROM controlte  WHERE idcte = '".$_SESSION['id']."'" ;
$controlte = mysqli_query($connect, $query);

$query = "SELECT * FROM control  WHERE idr = '".$_SESSION['id']."'" ;
$calificacion = mysqli_query($connect, $query);

$query = "SELECT * FROM seleccion  WHERE ids = '".$_SESSION['id']."'" ;
$seleccionado = mysqli_query($connect, $query);

$query = "SELECT * FROM monitoreo  WHERE idmon = '".$_SESSION['id']."'" ;
$tblmando = mysqli_query($connect, $query);

$query = "SELECT * FROM monitoreo  WHERE idmon = '".$_SESSION['id']."'" ;
$tblmando1 = mysqli_query($connect, $query);

$query = "SELECT * FROM monitoreo  WHERE idmon = '".$_SESSION['id']."'" ;
$tbdoc = mysqli_query($connect, $query);

$query = "SELECT * FROM monitoreo  WHERE idmon = '".$_SESSION['id']."'" ;
$tbdoca = mysqli_query($connect, $query);

$query = "SELECT * FROM monitoreo  WHERE idmon = '".$_SESSION['id']."'" ;
$requeridoc = mysqli_query($connect, $query);

$query = "SELECT * FROM monitoreo  WHERE idmon = '".$_SESSION['id']."'" ;
$prrp = mysqli_query($connect, $query);

$query = "SELECT * FROM monitoreo  WHERE idmon = '".$_SESSION['id']."'" ;
$sustentopago = mysqli_query($connect, $query);

while($susp = mysqli_fetch_array($sustentopago,MYSQLI_ASSOC))
{
	$_SESSION['ctrato']="Contrato";

	if($susp['contrato']=="Opcional"){ 
		$_SESSION['ctrato']="Orden de Compra";
	}elseif ($susp['contrato']=="Obligatorio") {
		$_SESSION['ctrato']="Contrato";
	}else{
		$_SESSION['ctrato']="Contrato";
	}

}

$_SESSION['cot1'] = "";
$_SESSION['cot2'] = "";
$_SESSION['cot3'] = "";

$connect2 = mysqli_connect("localhost", "root", "", "riesgo");
mysqli_set_charset($connect,"utf8");

$query = "SELECT * FROM usuarios WHERE matricula = '".$_SESSION['usuario']."'";
$nombres = mysqli_query($connect2, $query);

while($nomb = mysqli_fetch_array($nombres,MYSQLI_ASSOC))
{
	$servicio = $nomb['servicio'];
}

$connect3 = mysqli_connect("localhost", "root", "", "riesgoperativo");
mysqli_set_charset($connect3,"utf8");

$query = "SELECT * FROM servicio WHERE id_servicio = '$servicio'";
$ser = mysqli_query($connect3, $query);

while($servv = mysqli_fetch_array($ser,MYSQLI_ASSOC))
{
	$_SESSION['servicio'] = $servv['desc_servicio'];
	$area = $servv['id_division'];
}

$query = "SELECT * FROM division_area WHERE id_division = '$area'";
$sera = mysqli_query($connect3, $query);

while($servva = mysqli_fetch_array($sera,MYSQLI_ASSOC))
{
	$_SESSION['divarea'] = $servva['desc_division'];
}

$query = "SELECT * FROM legal_control  WHERE numero = '".$_SESSION['id']."'" ;
$resfirmado = mysqli_query($connect, $query);

$query = "SELECT * FROM legal_control  INNER JOIN solu_confl ON solu_confl.idsolu = legal_control.sol_conflictos WHERE legal_control.numero = '".$_SESSION['id']."'";
$fefr = mysqli_query($connect, $query);

$_SESSION['solucion'] = "";
while($repl = mysqli_fetch_array($fefr,MYSQLI_ASSOC))
{
	$_SESSION['solucion']= $repl['nombre'];
}

$query = "SELECT * FROM formulario  INNER JOIN tipoactividad ON tipoactividad.idtipoactividad = formulario.tac WHERE formulario.idf = '".$_SESSION['id']."'";
$qwer = mysqli_query($connect, $query);

$_SESSION['tac'] = "";
while($replas = mysqli_fetch_array($qwer,MYSQLI_ASSOC))
{
	$_SESSION['tac']= $replas['nombre'];
}

$query = "SELECT * FROM controlte WHERE idcte = '".$_SESSION['id']."'" ;
$controlado = mysqli_query($connect, $query);

$query = "SELECT * FROM controlte WHERE idcte = '".$_SESSION['id']."'" ;
$evtececo = mysqli_query($connect, $query);

while($evte = mysqli_fetch_array($evtececo,MYSQLI_ASSOC))
{
	$_SESSION['etecnico'] = $evte['et'];
	$_SESSION['teconomico'] = $evte['ee'];
	$_SESSION['tecnico'] = ($evte['et'] / 100);
	$_SESSION['economico'] = ($evte['ee'] / 100);
	$_SESSION['cp1'] = $evte['vp1'];
	$_SESSION['cp2'] = $evte['vp2'];
	$_SESSION['cp3'] = $evte['vp3'];
	$_SESSION['cp4'] = $evte['vp4'];
	$_SESSION['cp5'] = $evte['vp5'];

	$_SESSION['ccp1'] = $evte['pp1'];
	$_SESSION['ccp2'] = $evte['pp2'];
	$_SESSION['ccp3'] = $evte['pp3'];
	$_SESSION['ccp4'] = $evte['pp4'];
	$_SESSION['ccp5'] = $evte['pp5'];
	$_SESSION['cpm'] = $evte['vm'];
}

 ?> 

		
<!DOCTYPE html>
<html>
<head>
<title> >>SISTEMA DE PROVEEDORES<< </title>
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<meta http-equiv="Content-type" content="text/html; charset=utf-8">
<!-- <link href="http://fonts.googleapis.com/css?family=Open+Sans:400,300,600,700&subset=all" rel="stylesheet" type="text/css"/> -->
<link href="css/style.css" rel="stylesheet" type="text/css"/>

<link href="assets/global/plugins/font-awesome/css/font-awesome.min.css" rel="stylesheet" type="text/css"/>
<link href="assets/global/plugins/simple-line-icons/simple-line-icons.min.css" rel="stylesheet" type="text/css"/>
<link href="assets/global/plugins/bootstrap/css/bootstrap.min.css" rel="stylesheet" type="text/css"/>
<link href="assets/global/plugins/uniform/css/uniform.default.css" rel="stylesheet" type="text/css"/>
<link href="assets/global/plugins/icheck/skins/all.css" rel="stylesheet" type="text/css" />
<link href="assets/global/plugins/bootstrap-switch/css/bootstrap-switch.min.css" rel="stylesheet" type="text/css"/>
<link rel="stylesheet" type="text/css" href="assets/global/plugins/select2/select2.css"/>

<link href="assets/global/css/components-md.css" id="style_components" rel="stylesheet" type="text/css"/>
<link href="assets/global/css/plugins-md.css" rel="stylesheet" type="text/css"/>
<link href="assets/admin/layout/css/layout.css" rel="stylesheet" type="text/css"/>
<link id="style_color" href="assets/admin/layout/css/themes/darkblue.css" rel="stylesheet" type="text/css"/>
<link href="assets/admin/layout/css/custom.css" rel="stylesheet" type="text/css"/>
<link href="assets/global/plugins/bootstrap-modal/css/bootstrap-modal-bs3patch.css" rel="stylesheet" type="text/css"/>
<link href="assets/global/plugins/bootstrap-modal/css/bootstrap-modal.css" rel="stylesheet" type="text/css"/>

<link rel="stylesheet" type="text/css" href="assets/global/plugins/bootstrap-toastr/toastr.min.css"/>

<link href="assets/global/plugins/jquery-file-upload/blueimp-gallery/blueimp-gallery.min.css" rel="stylesheet"/>
<link href="assets/global/plugins/jquery-file-upload/css/jquery.fileupload.css" rel="stylesheet"/>
<link href="assets/global/plugins/jquery-file-upload/css/jquery.fileupload-ui.css" rel="stylesheet"/>
<link rel="shortcut icon" href="assets\admin\layout\img\sistema.png"/>
<link rel="stylesheet" type="text/css" href="css/listado_step.css">
</head>


<body>
<div class="page-header md-shadow-z-1-i navbar navbar-fixed-top">
	<div class="page-header-inner">
	
		<div class="page-logo">
			<a href="index.php">
			<img src="imagenes/prima.png" alt="logo" class="logo-default">
			</a>
			
		</div>
		<div class="top-menu">
			<ul class="nav navbar-nav pull-right">

				<li class="dropdown dropdown-extended dropdown-notification" id="header_notification_bar">
					<a href="inicio.php" class="dropdown-toggle" data-toggle="dropdown" data-hover="dropdown" data-close-others="true">
					<i class="fa fa-home"></i>
					</a>
				</li>

				<li class="dropdown dropdown-extended dropdown-notification" id="header_notification_bar">
					<a href="logout.php" class="dropdown-toggle" data-toggle="dropdown" data-hover="dropdown" data-close-others="true">
					<i class="fa fa-sign-out"></i>
					</a>
				</li>

				<li class="dropdown dropdown-user">
					<a href="javascript:;" class="dropdown-toggle" data-toggle="dropdown" data-hover="dropdown" data-close-others="true">
					<img alt="" class="img-circle" src="assets/admin/layout/img/avatar.png">
					<span class="username username-hide-on-mobile">
					<?php echo $_SESSION['nombre']; ?></span>

					</a>
				</li>
			</ul>
		</div>
	</div>
</div>
<div class="row">
	<div class="col-md-12" style="width: 110%;">
		<div class="portlet box blue">
			<div class="portlet-title">
				<div class="caption">
					<i class="fa fa-gift"></i> Gestión de Proveedores <span class="step-title">
					</span>
				</div>
			</div>	
		<div class="portlet-body form">
			<div class="form-horizontal">
			<div class="form-wizard">
				<div class="form-body">
					<ul class="nav nav-pills nav-justified steps">
						<li class="active" id="l1">
							<a  data-toggle="tab" class="step">
							<span class="number">
							1 </span>
							<span class="desc" style="font-size:100%;">
							<i class="fa fa-check"></i> Requerimiento</span>
							</a>
						</li>
						<li id="l2">
							<a  data-toggle="tab" class="step">
							<span class="number">
							2 </span>
							<span class="desc" style="font-size:100%;">
							<i class="fa fa-check"></i>Formulario</span>
							</a>
						</li>
						<li id="l3">
							<a  data-toggle="tab" class="step">
							<span class="number">
							3 </span>
							<span class="desc" style="font-size:100%;">
							<i class="fa fa-check"></i>Evaluación y Selección</span>
							</a>
						</li>
						<li id="l4">
							<a data-toggle="tab" class="step">
							<span class="number">
							4 </span>
							<span class="desc" style="font-size:100%;">
							<i class="fa fa-check"></i> Documentación </span>
							</a>
						</li>
						<li id="l5">
							<a  data-toggle="tab" class="step">
							<span class="number">
							5 </span>
							<span class="desc" style="font-size:100%;">
							<i class="fa fa-check"></i> Evaluación de Riesgos </span>
							</a>
						</li>
						<li id="l6">
							<a  data-toggle="tab" class="step">
							<span class="number">
							6 </span>
							<span class="desc" style="font-size:100%;">
							<i class="fa fa-check"></i><?php echo $_SESSION['ctrato'];?></span>
							</a>
						</li>
					</ul>
			<div class="tab-content">
				<div class="alert alert-danger display-none" id="error">
					<button type="button" class="close" data-dismiss="alert"></button>
					El requerimiento contiene campos incompletos o llenados incorrectamente, favor de verificar
				</div>
				<div class="alert alert-success display-none" id="correcto">
					<button type="button" class="close" data-dismiss="alert"></button>
					El requerimiento fue enviado con exito, queda pendiente su aprobación
				</div>
				<div class="alert alert-success display-none" id="info">
					<button type="button" class="close" data-dismiss="alert"></button>
					El requerimiento fue enviado con exito, queda pendiente su aprobación
				</div>
				<div class="alert alert-danger display-none" id="errorsubida">
					<button type="button" class="close" data-dismiss="alert"></button>
					Error al enviar los archivos, por favor verifique
				</div>
				<div class="alert alert-success display-none" id="subido">
					<button type="button" class="close" data-dismiss="alert"></button>
					La Carga se realizo con éxito!! 
				</div>

				<div class="alert alert-success display-none" id="form">
					<button type="button" class="close" data-dismiss="alert"></button>
					Formulario enviado con éxito!! 
				</div>

				<div class="alert alert-success display-none" id="evaluac">
					<button type="button" class="close" data-dismiss="alert"></button>
					Evaluación enviada con éxito!! 
				</div>

				<div class="alert alert-success display-none" id="reque">
					<button type="button" class="close" data-dismiss="alert"></button>
					Requerimiento enviado con éxito!! 
				</div>

				<div class="tab-pane active" id="tab1">

				<?php while($row = mysqli_fetch_array($result,MYSQLI_ASSOC) and $rows = mysqli_fetch_array($resultado,MYSQLI_ASSOC))
				{
				if($rows['acepre']==""){ 
				?>
				
					<form method="POST" id="formtab1" action="insert.php">
					<h4 class="block"><b>Registro de Requerimiento</b></h4>	

					<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">División/Área <span class="required">
						* </span>
						</label>
						<div class="col-md-2 divisiona">
									<select  class="form-control input-large select2m bg-blue-steel divisiona" data-placeholder="Select..." name="diva" id="diva" >
										<option value="" selected></option>

									</select>		
						</div>
					</div>
				</div>
					<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">Servicio <span class="required">
						* </span>
						</label>
						<div class="col-md-2 servicioa">
								<select  class="form-control input-large select2m servicioa" data-placeholder="Select..." name="serv" id="serv">
										<option value="" selected></option>

									</select>
						</div>
					</div>
				</div>
				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3" >Usuario <span class="required">
						* </span>
						</label>
						<div class="col-md-3">
							<input type="text" class="form-control input-large" name="usuario" id="usuario" value="<?php echo $_SESSION['nombre']; ?>" disabled/>
							<input type="text" class="form-control input-large" name="usuario2" id="usuario2" value="<?php echo $_SESSION['nombre']; ?>"  style="display:none"/>							
						</div>
					</div>
				</div>

				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">Fecha de Solicitud <span class="required">
						* </span>
						</label>
						<div class="col-md-3">
							<input type="date" class="form-control input-small" name="fecha" required/>			
						</div>
					</div>
				</div>

				<div class="col-md-6">	
					<div class="form-group">
						<label class="control-label col-md-3">Solicitud <span class="required">
						* </span>
						</label>
						<div class="col-md-3">
							<input type="text" class="form-control input-large" name="titulo" required />			
						</div>
					</div>
				</div>

				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">Descripción<span class="required">
						* </span>
						</label>
						<div class="col-md-3">
							<textarea class="form-control input-large" rows="3" name="descripcion" required></textarea>
							
						</div>
					</div>
				</div>
				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3" style="padding-right: 0px;" >Gasto aproximado Anual<span class="required">
						* </span>
						</label>
						<div class="col-md-1">
							<select class="form-control input-xsmall select2me" data-placeholder="Select..." name="moneda" id="moneda" required>
								<option value="S/." selected>S/.</option>
								<option value="$">$</option>
							</select>
						</div>
						<div class="col-md-3" style="left:2%;">
							<input type="text" style="text-align:right;" class="form-control input-small gsto" name="gastop" id="gastop" min="0.00" max="10000.00" step="0.01"required />
							<input type="text" class="form-control input-small" name="gasto" id="gasto" min="0.00" max="10000.00" step="0.01"required style="display:none;" />
						</div>						
						
					</div>
				</div>
				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3" style="padding-right: 0px;">¿Presupuesto aprobado? <span class="required">
						* </span>
						</label>
						<div class="col-md-2">
							<select class="form-control input-small select2me" data-placeholder="Select..." name="ppto" required>
								<option value=""></option>
								<option value="Si">Si</option>
								<option value="No">No</option>
							</select>
						</div>
					</div>
				</div>

				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">Bien / Servicio <span class="required">
						* </span>
						</label>
						<div class="col-md-2">
							<select class="form-control input-small select2me" data-placeholder="Select..." name="bs">
								<option value=""></option>
								<option value="Bien">Bien</option>
								<option value="Servicio">Servicio</option>

							</select>
						</div>
					</div>
				</div>
				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">Periodo de validez<span class="required">
						* </span>
						</label>
						<div class="col-md-2">
							<select class="form-control input-small select2me" data-placeholder="Select..." name="periodo">
								<option value=""></option>
								<option value="Única vez">Única vez</option>
								<option value="Permanente">Permanente</option>
							</select>
						</div>
					</div>
				</div>
				<div class="row">
					<div class="col-md-offset-5 col-md-8">
						<input type="submit" name="solicita" id="solicita" position="center" class="btn btn-success" value="Solicitar"> 	
					</div>
				</div>
				</form>

				<div class="form-actions">
					<div class="row-a">
						<div class="col-md-1" style="display:none;" id="atras">
							<a href="javascript:;" class="btn blue button-previous" >
							<i class="m-icon-swapleft m-icon-white"></i></a>
						</div>
						<div class="col-md-1" style="display:none" id="siguiente">				
							<a href="javascript:;" class="btn green button-next" >
							<i class="m-icon-swapright m-icon-white"></i>
							</a>
						</div>
						<div class="col-md-offset-1 col-md-9" style="display:none" id="fin">
							<a href="javascript:;" class="btn yellow button-submit">
							Finalizar <i class="m-icon-swapright m-icon-white"></i>  
							</a>
							
						</div>
					</div>
				</div>

				<?php

				}else if($rows['acepre']=='no'){

				?>
				<form method="POST" id="formtab1" action="insert.php">
				<h4 class="block"><b>Registro de Requerimiento</b></h4>	
				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">División/Área <span class="required">
						* </span>
						</label>
						<div class="col-md-2">
									<select  class="form-control input-large select2m" data-placeholder="Select..." name="diva" id="diva" readonly>
										<option value="<?php echo $row['divarea'];?>" selected><?php echo $row['divarea'];?></option>

									</select>	
						</div>
					</div>
				</div>
				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3" >Usuario <span class="required">
						* </span>
						</label>
						<div class="col-md-3">
							<input type="text" class="form-control input-large" name="usuario" id="usuario" value="<?php echo $row['usuario']; ?>" disabled/>
							<input type="text" class="form-control input-large" name="usuario2" id="usuario2" value="<?php echo $row['usuario']; ?>"  style="display:none"/>					
						</div>
					</div>
				</div>
				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">Servicio <span class="required">
						* </span>
						</label>
						<div class="col-md-2 servicioa">
								<select  class="form-control input-large select2m servicioa" data-placeholder="Select..." name="serv" id="serv" readonly>
										<option value="<?php echo $row['servicio'];?>" selected><?php echo $row['servicio'];?></option>

									</select>
						</div>
					</div>
				</div>
				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">Fecha de Solicitud <span class="required">
						* </span>
						</label>
						<div class="col-md-3">
							<input type="date" style="padding-right: 0px;" class="form-control" name="fecha" required value="<?php echo $row['fecha'];?>"/>		
						</div>
					</div>
				</div>
				<div class="row"><hr></div>
				<div class="col-md-6">	
					<div class="form-group">
						<label class="control-label col-md-3">Solicitud <span class="required">
						* </span>
						</label>
						<div class="col-md-3">
							<input type="text" class="form-control" name="titulo" value="<?php echo $row['titulo'];?>" required />			
						</div>
					</div>
				</div>
				<div class="row" style="margin-top:0px"></div>
				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">Descripción<span class="required">
						* </span>
						</label>
						<div class="col-md-3">
							<textarea class="form-control" rows="3" name="descripcion" required style="	width:670%;"><?php echo $row['descrip'];?></textarea>
							
						</div>
					</div>
				</div>
				<div class="row">	</div>
				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3" style="padding-right: 0px;" >Gasto aproximado Total<span class="required">
						* </span>
						</label>
						<div class="col-md-1">
							<select class="form-control input-xsmall select2me" data-placeholder="Select..." name="moneda" id="moneda" required>
								<?php if ($row['monedaa'] == "$") { ?>
								<option value="S/.">S/.</option>
								<option value="$"  selected>$</option>

								<?php
								} else{?>
								<option value="S/." selected>S/.</option>
								<option value="$">$</option>
								<?php
								}?>
							</select>
						</div>
						<div class="col-md-3" style="left:2%;">
							<input type="text" class="form-control input-medium" style="text-align:right;" name="gasto" value="<?php echo $row['gastoanual'];?>" required />	
						</div>						
						
					</div>
				</div>

				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3" style="padding-right: 0px;" >Gasto aproximado Anual<span class="required">
						* </span>
						</label>
						<div class="col-md-1">
							<select class="form-control input-xsmall select2me" data-placeholder="Select..." name="monedaa" id="monedaa" required>
								<?php if ($row['tipo_moneda'] == "$") { ?>
								<option value="S/.">S/.</option>
								<option value="$"  selected>$</option>

								<?php
								} else{?>
								<option value="S/." selected>S/.</option>
								<option value="$">$</option>
								<?php
								}?>
							</select>
						</div>
						<div class="col-md-3" style="left:2%;">
							<input type="text" class="form-control input-medium" style="text-align:right;" name="gasto" value="<?php echo $row['gasto'];?>" required />	
						</div>						
						
					</div>
				</div>

				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">¿Presupuesto aprobado?<span class="required">
						* </span>
						</label>
						<div class="col-md-2">
							<select class="form-control input-small select2me" data-placeholder="Select..." name="ppto" required>
								<?php if ($row['pres'] == "Si") { ?>
								<option value="Si" selected>Si</option>
								<option value="No">No</option>

								<?php
								} else{?>
								<option value="Si">Si</option>
								<option value="No" selected>No</option>
								<?php
								}?>
							</select>
						</div>
					</div>
				</div>

				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">Clasificación Inversión/Gasto<span class="required">
						* </span>
						</label>
						<div class="col-md-2">
							<select class="form-control input-large select2me" data-placeholder="Select..." name="clasif" id="clasif">
								<option value="<?php echo $row['periodo'];?>" selected><?php echo $row['periodo'];?></option>
								<option value="Gasto">Gasto</option>
								<option value="Inversión activo fijo">Inversión activo fijo</option>
								<option value="Inversión sistemas">Inversión sistemas</option>
							</select>
						</div>
					</div>
				</div>

				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">Bien / Servicio <span class="required">
						* </span>
						</label>
						<div class="col-md-2">
							<select class="form-control input-large select2me" data-placeholder="Select..." name="bs">
								<option value="<?php echo $row['biens'];?>" selected><?php echo $row['biens'];?></option>
								<option value="Bien">Bien</option>
								<option value="Servicio">Servicio</option>

							</select>
						</div>
					</div>
				</div>

				<div class="row" style="margin-top:0px"></div>
				<div class="row" style="margin-top:0px"><hr></div>
				<div class="col-md-6">
					<div class="form-group" style="text-align:center;">
						<div class="control-label col-md-3" style="">
							<label>Comentario <span class="required" style="color:red">
						* </span></label>
						</div>
						<div class="col-md-3">
						<textarea placeholder="Comentario..." id="comm" name="comm" class="form-control" style="margin: 0px;width: 670%;height: 86px;" required><?php echo $row['comm'];?></textarea>	
						</div>
						
					</div>
					<label style="color:red;">&nbsp;Los campos que contengan <b>(*)</b> Son de caracter obligatorio</label>
				</div>
				<div class="row"  id="solicita1" style="display:block;">
					<div class="col-md-offset-5 col-md-8">
						<input type="submit" name="insertar" id="insertar" position="center" class="btn btn-success" value="Solicitar"> 	
					</div>
				</div>
				</form>

				<div class="form-actions">
					<div class="row-a">
						<div class="col-md-1" style="display:none;" id="atras">
							<a href="javascript:;" class="btn blue button-previous">
							<i class="m-icon-swapleft m-icon-white"></i></a>
						</div>
						<div class="col-md-1" style="display:none" id="siguiente">				
							<a href="javascript:;" class="btn green button-next">
							<i class="m-icon-swapright m-icon-white"></i>
							</a>
						</div>
						<div class="col-md-offset-1 col-md-9" style="display:none" id="fin">
							<a href="javascript:;" class="btn yellow button-submit">
							Finalizar <i class="m-icon-swapright m-icon-white"></i>  
							</a>
							
						</div>
					</div>
				</div>

				<?php
				}else {
				?>
					<h4 class="block"><b>Registro de Requerimiento</b></h4>

					<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">División/Área <span class="required">
						* </span>
						</label>
						<div class="col-md-2">
							<input type="text" class="form-control input-large" name="diva" id="diva" value="<?php echo $row['divarea'];?>" readonly/>
							<input type="text" class="form-control input-large" name="diva" id="diva" value="<?php echo $row['divarea'];?>"  style="display:none"/>		
						</div>
					</div>
					</div>

				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3" >Usuario <span class="required">
						* </span>
						</label>
						<div class="col-md-3">
							<input type="text" class="form-control input-large" name="usuario" id="usuario" style="text-transform:capitalized;" value="<?php echo $row['usuario']; ?>" disabled/>
							<input type="text" class="form-control" name="usuario2" id="usuario2" value="<?php echo $row['usuario']; ?>"  style="display:none"/>							
						</div>
					</div>
				</div>

					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-3">Servicio <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<input type="text" class="form-control input-large" name="serv" id="serv" value="<?php echo $row['servicio'];?>" readonly/>
								<input type="text" class="form-control input-large" name="serv" id="serv" value="<?php echo $row['servicio'];?>"  style="display:none"/>
							</div>
						</div>
					</div>


				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">Fecha de Solicitud <span class="required">
						* </span>
						</label>
						<div class="col-md-3">
							<input type="text" class="form-control input-large" name="fecha" id="fecha" value="<?php echo $row['fecha'];?>" readonly/>
							<input type="text" class="form-control"  value="<?php echo $row['fecha'];?>"  style="display:none"/>			
						</div>
					</div>
				</div>
				<div class="row"><hr></div>
				<div class="col-md-6">	
					<div class="form-group">
						<label class="control-label col-md-3">Solicitud <span class="required">
						* </span>
						</label>
						<div class="col-md-6">
							<input type="text" class="form-control input-large" name="titulo" id="titulo" value="<?php echo $row['titulo'];?>" readonly/>
							<input type="text" class="form-control" name="titulo" id="titulo" value="<?php echo $row['titulo'];?>"  style="display:none"/>		
						</div>
					</div>
				</div>
				<div class="row" style="margin-top:0px"></div>
				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">Descripción<span class="required">
						* </span>
						</label>
						<div class="col-md-3">
							<textarea class="form-control" rows="3" name="descripcion" readonly style="width:670%;"><?php echo $row['descrip'];?></textarea>
						</div>
					</div>
				</div>
				<div class="row">	</div>
				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3" style="padding-right: 0px;" >Gasto aproximado Total<span class="required">
						* </span>
						</label>
						<div class="col-md-1">
							<input type="text" class="form-control input-xsmall" style="text-align:right;" name="moneda" id="moneda" value="<?php echo $row['monedaa'];?>" readonly/>
							<input type="text" class="form-control input-small" name="moneda" id="moneda" value="<?php echo $row['monedaa'];?>"  style="display:none" />
						</div>
						<div class="col-md-3" style="left:2%;">
							<input type="text" class="form-control input-medium" style="text-align:right;" name="gasto" id="gasto" value="<?php echo $row['gastoanual'];?>" readonly/>
							<input type="text" class="form-control" name="gasto" id="gasto" value="<?php echo $row['gastoanual'];?>"  style="display:none"/>	
						</div>						
						
					</div>
				</div>

				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3" style="padding-right: 0px;" >Gasto aproximado Anual<span class="required">
						* </span>
						</label>
						<div class="col-md-1">
							<input type="text" class="form-control input-xsmall" style="text-align:right;" name="monedaa" id="monedaa" value="<?php echo $row['tipo_moneda'];?>" readonly/>
							<input type="text" class="form-control input-small" name="moneda" id="moneda" value="<?php echo $row['tipo_moneda'];?>"  style="display:none" />
						</div>
						<div class="col-md-3" style="left:2%;">
							<input type="text" class="form-control input-medium" style="text-align:right;" name="gastop" id="gastop" value="<?php echo $row['gasto'];?>" readonly/>
							<input type="text" class="form-control" name="gastoanual" id="gastoanual" value="<?php echo $row['gasto'];?>"  style="display:none"/>	
						</div>						
						
					</div>
				</div>
				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3" style="padding-right: 0px;">¿Presupuesto aprobado?<span class="required">
						* </span>
						</label>
						<div class="col-md-2">
							<input type="text" class="form-control input-large" name="ppto" id="ppto" value="<?php echo $row['pres'];?>" readonly/>
							<input type="text" class="form-control input-small" name="ppto" id="ppto" value="<?php echo $row['pres'];?>"  style="display:none"/>
						</div>
					</div>
				</div>

				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">Clasificación Inversión/Gasto<span class="required">
						* </span>
						</label>
						<div class="col-md-2">
							<input type="text" class="form-control input-large" name="periodo" id="periodo" value="<?php echo $row['periodo'];?>" readonly/>
							<input type="text" class="form-control input-small" name="periodo" id="periodo" value="<?php echo $row['periodo'];?>"  style="display:none"/>
						</div>
					</div>
				</div>

				<div class="col-md-6">
					<div class="form-group">
						<label class="control-label col-md-3">Bien / Servicio <span class="required">
						* </span>
						</label>
						<div class="col-md-2">
							<input type="text" class="form-control input-large" name="bs" id="bs" value="<?php echo $row['biens'];?>" readonly/>
							<input type="text" class="form-control input-small" name="bs" id="bs" value="<?php echo $row['biens'];?>"  style="display:none"/>
						</div>
					</div>
				</div>

				<div class="row" style="margin-top:0px"></div>
				<div class="row" style="margin-top:0px"><hr></div>
				<div class="col-md-6">
					<div class="form-group" style="text-align:center;">
						<div class="control-label col-md-3" style="">
							<label>Comentario <span class="required" style="color:red">
						* </span></label>
						</div>
						<div class="col-md-3">
						<textarea placeholder="Comentario..." id="comm" name="comm" class="form-control" style="margin: 0px;width: 670%;" rows="3" readonly="readonly"><?php echo $row['comm'];?></textarea>	
						</div>
						
					</div>
					<label style="color:red;">&nbsp;Los campos que contengan <b>(*)</b> Son de caracter obligatorio</label>
				</div>
				<div class="row" style="margin-top:0px"></div>
				<?php 
				if($rows['acepre'] =='si'){
					?>
				<div class="form-actions">
					<div class="row-a">
						<div class="col-md-1" style="display:none;" id="atras">
							<a href="javascript:;" class="btn blue button-previous" >
							<i class="m-icon-swapleft m-icon-white"></i></a>
						</div>
						<div class="col-md-1" style="display:block; float: right;" id="siguiente">				
							<a href="javascript:;" class="btn green button-next" >
							<i class="m-icon-swapright m-icon-white"></i>
							</a>
						</div>
						<div class="col-md-offset-1 col-md-9" style="display:none" id="fin">
							<a href="javascript:;" class="btn yellow button-submit">
							Finalizar <i class="m-icon-swapright m-icon-white"></i>  
							</a>
							
						</div>
					</div>
				</div>
				<?php
					} else{
						?>
						<div class="form-actions">
					<div class="row-a">
						<div class="col-md-1" style="display:none;" id="atras">
							<a href="javascript:;" class="btn blue button-previous">
							<i class="m-icon-swapleft m-icon-white"></i></a>
						</div>
						<div class="col-md-1" style="display:none" id="siguiente">				
							<a href="javascript:;" class="btn green button-next">
							<i class="m-icon-swapright m-icon-white"></i>
							</a>
						</div>
						<div class="col-md-offset-1 col-md-9" style="display:none" id="fin">
							<a href="javascript:;" class="btn yellow button-submit">
							Finalizar <i class="m-icon-swapright m-icon-white"></i>  
							</a>
							
						</div>
					</div>
				</div>
						<?php
					}
				?>
				<?php
				}
		}?>
		</div>

		<div class="tab-pane" id="tab2" >
		<?php 
		while($rows = mysqli_fetch_array($resultado3,MYSQLI_ASSOC) and $row = mysqli_fetch_array($resultado2,MYSQLI_ASSOC)){
				{
				if($rows['acepfor']==""){ 
				?>
					<form method="POST" id="formtab2" action="insert2.php">
						<h4 class="block" ><b>Evaluación y Selección del Proveedor</b></h4>
						<label style="font-size:12px;"><b>Completar los campos a fin de determinar la dimensión del servicio o bien requerido</b></label>	
						<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">Macroproceso<span class="required">
							* </span>
							</label>
							<div class="col-md-2 macroproceso">
								<select class="form-control input-large select2me macroproceso" data-placeholder="Select..." name="macro" id="macro" required>
									<option value="" selected></option>

								</select>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">Proceso <span class="required">
							* </span>
							</label>
							<div class="col-md-2 proceso">
								<select class="form-control input-large select2me proceso" data-placeholder="Select..." name="proce" required>
									<option value="" selected></option>

								</select>
							</div>
						</div>
					</div>
					
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">¿Procesamiento de datos en el exterior? <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="ext" required>
									<option value="" selected></option>
									<option value="Si">Si</option>
									<option value="No">No</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">¿Contratación Corporativa? <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="corp" required>
									<option value="" selected></option>
									<option value="Si">Si</option>
									<option value="No">No</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">¿Desarrollo de actividades dentro de Prima? <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="dact" required>
									<option value="" selected></option>
									<option value="Si">Si</option>
									<option value="No">No</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">¿Prima es sujeto de Supervisión / Regulación? <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="supreg" required>
									<option value="" selected></option>
									<option value="Si">Si</option>
									<option value="No">No</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">Tipo de Actividad a Contratar <span class="required">
							* </span>
							</label>
							<div class="col-md-2 tacontratar">
								<select class="form-control input-small select2me tacontratar" data-placeholder="Select..." name="tac" id ="tac" required>
									<option value="" selected></option>
								</select>
							</div>
						</div>
					</div>
					<div class="row">
						
					</div>
					<h4 class="block"  style="text-decoration: underline;">Definición del Impacto</h4>
				

						<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">La interrupción del bien/servicio prestado qué tipo de impacto generaría en la continuidad operativa</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="timp" required>
									<option value="" selected></option>
									<option value="Bajo">Bajo</option>
									<option value="Moderado">Moderado</option>
									<option value="Relevante">Relevante</option>
									<option value="Alto">Alto</option>
									<option value="Crítico">Crítico</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">Qué tipo de información de Prima AFP o sus clientes será administrada por el proveedor</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="info" required>
									<option value="" selected></option>
									<option value="No Aplica">No Aplica</option>
									<option value="Uso Público">Uso Público</option>
									<option value="Uso Interno">Uso Interno</option>
									<option value="Confidencial">Confidencial</option>
								</select>
							</div>
					
					</div>
						</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">La interrupción del bien/servicio prestado podría llevar a un riesgo reputacional de qué nivel</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="rrep" required>
									<option value="" selected></option>
									<option value="Bajo">Bajo</option>
									<option value="Moderado">Moderado</option>
									<option value="Relevante">Relevante</option>
									<option value="Alto">Alto</option>
									<option value="Crítico">Crítico</option>
								</select>
							</div>
						</div>
						</div>
						<div class="row"></div>
					<h4 class="block"  style="text-decoration: underline;">Definición de la Criticidad</h4>
			
						<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">La cantidad de proveedores en el mercado que pueden brindar el bien/servicio deseado en el mercado</label>
							<div class="col-md-2">
								<select class="form-control input-slarge select2me" data-placeholder="Select..." name="cant" required>
									<option value="" selected></option>
									<option value="1 Proveedor">1 Proveedor</option>
									<option value="Hasta 2 Proveedores">Hasta 2 Proveedores</option>
									<option value="Hasta 3 Proveedores">Hasta 3 Proveedores</option>
									<option value="Hasta 4 Proveedores">Hasta 4 Proveedores</option>
									<option value="Más de 4 Proveedores">Más de 4 Proveedores</option>
									
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">El cambiar de proveedor qué nivel de impacto negativo podría generar en Prima AFP</label>
							<div class="col-md-2">
								<select class="form-control input-slarge select2me" data-placeholder="Select..." name="impn" required>
									<option value="" selected></option>
									<option value="Ningún Impacto">Ningún Impacto</option>
									<option value="Bajo Impacto">Bajo Impacto</option>
									<option value="Mediano Impacto">Mediano Impacto</option>
									<option value="Alto Impacto">Alto Impacto</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">La relación del bien o servicio a contratar será de  ...</label>
							<div class="col-md-2">
								<select class="form-control input-slarge select2me" data-placeholder="Select..." name="rela" required>
									<option value="" selected></option>
									<option value="Única vez">Única vez</option>
									<option value="Corto Plazo">Corto Plazo</option>
									<option value="Mediano Plazo">Mediano Plazo</option>
									<option value="Largo Plazo">Largo Plazo</option>
								</select>
							</div>
						</div>
					</div>
					<div class="row">
					<div class="col-md-offset-6 col-md-8">
						<input type="submit" name="reg" id="reg" position="center" class="btn btn-success" value="Registrar"> 	
					</div>
				</div>
				</form>

				<div class="form-actions">
					<div class="row-a">
						<div class="col-md-1" style="display:block;" id="atras1">
							<a href="javascript:;" class="btn blue button-previous">
							<i class="m-icon-swapleft m-icon-white"></i></a>
						</div>
						<div class="col-md-1" style="display:none" id="siguiente1" value="inicial">				
							<a href="javascript:;" class="btn green button-next">
							<i class="m-icon-swapright m-icon-white"></i>
							</a>
						</div>
						<div class="col-md-offset-1 col-md-9" style="display:none" id="fin1">
							<a href="javascript:;" class="btn yellow button-submit" id="fin">
							Finalizar <i class="m-icon-swapright m-icon-white"></i>  
							</a>
							
						</div>
					</div>
				</div>
				<label style="color:red;">&nbsp;Los campos que contengan <b>(*)</b> Son de caracter obligatorio</label>	
				<?php
				}else if($rows['acepfor']=='no'){
				?>
					
					<form method="POST" id="formtab2" action="insert2.php">
						<h4 class="block" ><b>Evaluación y Selección del Proveedor</b></h4>
						<label style="font-size:12px;"><b>Completar los campos a fin de determinar la dimensión del servicio o bien requerido</b></label>
						<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">Macroproceso<span class="required">
							* </span>
							</label>
							<div class="col-md-2 macroproceso">
								<select class="form-control input-large select2me macroproceso" data-placeholder="Select..." name="macro" id="macro" required>
									<option value="<?php echo $row['macro'];?>" selected><?php echo $row['macro'];?></option>

								</select>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">Proceso <span class="required">
							* </span>
							</label>
							<div class="col-md-2 proceso">
								<select class="form-control input-large select2me proceso" data-placeholder="Select..." name="proce" required>
									<option value="<?php echo $row['proce'];?>" selected><?php echo $row['proce'];?></option>

								</select>
							</div>
						</div>
					</div>
					
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">¿Procesamiento de datos en el exterior? <span class="required" >
							* </span>
							</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="ext" required>
									<option value="<?php echo $row['ext'];?>" selected><?php echo $row['ext'];?></option>
									<option value="Si">Si</option>
									<option value="No">No</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">¿Contratación Corporativa? <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="corp" required>
									<option value="<?php echo $row['corp'];?>" selected><?php echo $row['corp'];?></option>
									<option value="Si">Si</option>
									<option value="No">No</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">¿Desarrollo de actividades dentro de Prima? <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="dact" required>
									<option value="<?php echo $row['dact'];?>" selected><?php echo $row['dact'];?></option>
									<option value="Si">Si</option>
									<option value="No">No</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">¿Prima es sujeto de Supervisión / Regulación? <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="supreg" required>
									<option value="<?php echo $row['dact'];?>" selected><?php echo $row['supreg'];?></option>
									<option value="Si">Si</option>
									<option value="No">No</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">Tipo de Actividad a Contratar <span class="required">
							* </span>
							</label>
							<div class="col-md-2 tacontratar">
								<select class="form-control input-large select2me tacontratar" data-placeholder="Select..." name="tac" id ="tac" required>
									<option value="<?php echo $_SESSION['tac'];?>" selected><?php echo $_SESSION['tac'];?></option>
								</select>
							</div>
						</div>
					</div>
					<div class="row">
						
					</div>
					<h4 class="block"  style="text-decoration: underline;">Definición del Impacto</h4>
				

						<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">La interrupción del bien/servicio prestado qué tipo de impacto generaría en la continuidad operativa</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="timp" required>
									<option value="<?php echo $row['timp'];?>" selected><?php echo $row['timp'];?></option>
									<option value="Bajo">Bajo</option>
									<option value="Moderado">Moderado</option>
									<option value="Relevante">Relevante</option>
									<option value="Alto">Alto</option>
									<option value="Crítico">Crítico</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">Qué tipo de información de Prima AFP o sus clientes será administrada por el proveedor</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="info" required>
									<option value="<?php echo $row['info'];?>" selected><?php echo $row['info'];?></option>
									<option value="No Aplica">No Aplica</option>
									<option value="Uso Público">Uso Público</option>
									<option value="Uso Interno">Uso Interno</option>
									<option value="Confidencial">Confidencial</option>
								</select>
							</div>
					
					</div>
						</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">La interrupción del bien/servicio prestado podría llevar a un riesgo reputacional de qué nivel</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="rrep" required>
									<option value="<?php echo $row['rrep'];?>" selected><?php echo $row['rrep'];?></option>
									<option value="Bajo">Bajo</option>
									<option value="Moderado">Moderado</option>
									<option value="Relevante">Relevante</option>
									<option value="Alto">Alto</option>
									<option value="Crítico">Crítico</option>
								</select>
							</div>
						</div>
						</div>
						<div class="row"></div>
					<h4 class="block"  style="text-decoration: underline;">Definición de la Criticidad</h4>
			
						<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">La cantidad de proveedores en el mercado que pueden brindar el bien/servicio deseado en el mercado</label>
							<div class="col-md-2">
								<select class="form-control input-slarge select2me" data-placeholder="Select..." name="cant" required>
									<option value="<?php echo $row['cant'];?>" selected><?php echo $row['cant'];?></option>
									<option value="1 Proveedor">1 Proveedor</option>
									<option value="Hasta 2 Proveedores">Hasta 2 Proveedores</option>
									<option value="Hasta 3 Proveedores">Hasta 3 Proveedores</option>
									<option value="Hasta 4 Proveedores">Hasta 4 Proveedores</option>
									<option value="Más de 4 Proveedores">Más de 4 Proveedores</option>
									
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">El cambiar de proveedor qué nivel de impacto negativo podría generar en Prima AFP</label>
							<div class="col-md-2">
								<select class="form-control input-slarge select2me" data-placeholder="Select..." name="impn" required>
									<option value="<?php echo $row['impn'];?>" selected><?php echo $row['impn'];?></option>
									<option value="Ningún Impacto">Ningún Impacto</option>
									<option value="Bajo Impacto">Bajo Impacto</option>
									<option value="Mediano Impacto">Mediano Impacto</option>
									<option value="Alto Impacto">Alto Impacto</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">La relación del bien o servicio a contratar será de  ...</label>
							<div class="col-md-2">
								<select class="form-control input-slarge select2me" data-placeholder="Select..." name="rela" required>
									<option value="<?php echo $row['rela'];?>" selected><?php echo $row['rela'];?></option>
									<option value="Única vez">Única vez</option>
									<option value="Corto Plazo">Corto Plazo</option>
									<option value="Mediano Plazo">Mediano Plazo</option>
									<option value="Largo Plazo">Largo Plazo</option>
								</select>
							</div>
						</div>
					</div>
					<div class="row">
					<div class="col-md-offset-6 col-md-8">
						<input type="submit" name="reg1" id="reg1" position="center" class="btn btn-success" value="Registrar"> 	
					</div>
				</div>
				</form>

				<div class="form-actions">
					<div class="row-a">
						<div class="col-md-1" style="display:block;" id="atras1">
							<a href="javascript:;" class="btn blue button-previous">
							<i class="m-icon-swapleft m-icon-white"></i></a>
						</div>
						<div class="col-md-1" style="display:none" id="siguiente1">				
							<a href="javascript:;" class="btn green button-next">
							<i class="m-icon-swapright m-icon-white"></i>
							</a>
						</div>
						<div class="col-md-offset-1 col-md-9" style="display:none" id="fin1">
							<a href="javascript:;" class="btn yellow button-submit" id="fin">
							Finalizar <i class="m-icon-swapright m-icon-white"></i>  
							</a>
							
						</div>
					</div>
				</div>


				<?php
				} else {
				?>
				<div>
					<h4 class="block" ><b>Evaluación y Selección del Proveedor</b></h4>
				<label style="font-size:13px;margin-left:1%;color:grey"><b>Los campos se completaron con el fin de determinar la dimensión del servicio o bien requerido</b>
				</label>
				
				</div>
				<br>
				
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">Macroproceso<span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<input type="text" class="form-control input-large" name="macro" id="macro" value="<?php echo $row['macro'];?>" readonly/>
								<input type="text" class="form-control input-large" name="macro" id="macro" value="<?php echo $row['macro'];?>"  style="display:none"/>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">Proceso <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<input type="text" class="form-control input-large" name="proce" id="proce" value="<?php echo $row['proce'];?>" readonly/>
								<input type="text" class="form-control input-large" name="proce" id="proce" value="<?php echo $row['proce'];?>"  style="display:none"/>
							</div>
						</div>
					</div>
					
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">¿Procesamiento de datos en el exterior? <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<input type="text" class="form-control input-small" name="ext" id="ext" value="<?php echo $row['ext'];?>" readonly/>
								<input type="text" class="form-control input-small" name="ext" id="ext" value="<?php echo $row['ext'];?>"  style="display:none"/>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">¿Contratación Corporativa? <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<input type="text" class="form-control input-small" name="corp" id="corp" value="<?php echo $row['corp'];?>" readonly/>
								<input type="text" class="form-control input-small" name="corp" id="corp" value="<?php echo $row['corp'];?>"  style="display:none"/>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">¿Desarrollo de actividades dentro de Prima? <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<input type="text" class="form-control input-small" name="dact" id="dact" value="<?php echo $row['dact'];?>" readonly/>
								<input type="text" class="form-control input-small" name="dact" id="dact" value="<?php echo $row['dact'];?>"  style="display:none"/>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">¿Prima es sujeto de Supervisión / Regulación? <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<input type="text" class="form-control input-small" name="supreg" id="supreg" value="<?php echo $row['supreg'];?>" readonly/>
								<input type="text" class="form-control input-small" name="supreg" id="supreg" value="<?php echo $row['supreg'];?>"  style="display:none"/>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">Tipo de Actividad a Contratar <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<input type="text" class="form-control input-large" name="tac" id="tac" value="<?php echo $_SESSION['tac'];?>" readonly/>
								<input type="text" class="form-control input-large" name="tac" id="tac" value="<?php echo $_SESSION['tac'];?>" style="display:none;"/>
							</div>
						</div>
					</div>
					<div class="row">
						
					</div>
					<div class="col-md-12">
					<h4 class="block"  style="text-decoration: underline;">Definición del Impacto</h4>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">La interrupción del bien/servicio prestado qué tipo de impacto generaría en la continuidad operativa</label>
							<div class="col-md-2">
								<input type="text" class="form-control input-small" name="timp" id="timp" value="<?php echo $row['timp'];?>" readonly/>
								<input type="text" class="form-control input-small" name="timp" id="timp" value="<?php echo $row['timp'];?>"  style="display:none"/>
							</div>
						</div>
					</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">Qué tipo de información de Prima AFP o sus clientes será administrada por el proveedor</label>
							<div class="col-md-2">
								<input type="text" class="form-control input-small" name="info" id="info" value="<?php echo $row['info'];?>" readonly/>
								<input type="text" class="form-control input-small" name="info" id="info" value="<?php echo $row['info'];?>"  style="display:none"/>
							</div>
					
						</div>
					</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">La interrupción del bien/servicio prestado podría llevar a un riesgo reputacional de qué nivel</label>
							<div class="col-md-2">
								<input type="text" class="form-control input-small" name="rrep" id="rrep" value="<?php echo $row['rrep'];?>" readonly/>
								<input type="text" class="form-control input-small" name="rrep" id="rrep" value="<?php echo $row['rrep'];?>"  style="display:none"/>
							</div>
						</div>
					</div>
					<div class="row"></div>
					<div class="col-md-12">
					<h4 class="block col-md-6"  style="text-decoration: underline;padding-left: 0px;">Definición de la Criticidad</h4>

					<button class="btn blue" style="left: 30%;" onclick="tipop()"> Ver Condiciones del Proveedor </button>
							
					</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">La cantidad de proveedores en el mercado que pueden brindar el bien/servicio deseado en el mercado</label>
							<div class="col-md-2">
								<input type="text" class="form-control input-slarge" name="cant" id="cant" value="<?php echo $row['cant'];?>" readonly/>
								<input type="text" class="form-control input-large" name="cant" id="cant" value="<?php echo $row['cant'];?>"  style="display:none"/>
							</div>
						</div>
					</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">El cambiar de proveedor qué nivel de impacto negativo podría generar en Prima AFP</label>
							<div class="col-md-2">
								<input type="text" class="form-control input-slarge" name="impn" id="impn" value="<?php echo $row['impn'];?>" readonly/>
								<input type="text" class="form-control input-large" name="impn" id="impn" value="<?php echo $row['impn'];?>"  style="display:none"/>
							</div>
						</div>
					</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">La relación del bien o servicio a contratar será de  ...</label>
							<div class="col-md-2">
								<input type="text" class="form-control input-slarge" name="rela" id="rela" value="<?php echo $row['rela'];?>" readonly/>
								<input type="text" class="form-control input-small" name="rela" id="rela" value="<?php echo $row['rela'];?>"  style="display:none"/>
							</div>
						</div>
					</div>
					<label style="color:red;">&nbsp;Todos los campos son de caracter obligatorio</label>	
				
			<?php

				if($rows['acepfor'] =='si'){

					?>
				<div class="form-actions">
					<div class="row-a">
						<div class="col-md-1" style="display:block;" id="atras1">
							<a href="javascript:;" class="btn blue button-previous" id="atras">
							<i class="m-icon-swapleft m-icon-white"></i></a>
						</div>
						<div class="col-md-1" style="display:block; float: right;" id="siguiente1" value="inicial">				
							<a href="javascript:;" class="btn green button-next" id="siguiente">
							<i class="m-icon-swapright m-icon-white"></i>
							</a>
						</div>
						<div class="col-md-offset-1 col-md-9" style="display:none" id="fin1">
							<a href="javascript:;" class="btn yellow button-submit" id="fin">
							Finalizar <i class="m-icon-swapright m-icon-white"></i>  
							</a>
							
						</div>
					</div>
				</div>
				<?php
					} else{
						?>
				<div class="form-actions">
					<div class="row-a">
						<div class="col-md-1" style="display:block;" id="atras1">
							<a href="javascript:;" class="btn blue button-previous">
							<i class="m-icon-swapleft m-icon-white"></i></a>
						</div>
						<div class="col-md-1" style="display:none" id="siguiente1">				
							<a href="javascript:;" class="btn green button-next">
							<i class="m-icon-swapright m-icon-white"></i>
							</a>
						</div>
						<div class="col-md-offset-1 col-md-9" style="display:none" id="fin1">
							<a href="javascript:;" class="btn yellow button-submit" id="fin">
							Finalizar <i class="m-icon-swapright m-icon-white"></i>  
							</a>
							
						</div>
					</div>
				</div>
						<?php
					}
				?>
			<?php
			}
		}
	}
	if(mysqli_num_rows($resultado2)< 1){
		?>
	 	<form method="POST" id="formtab2" action="insert2.php">
						<div>
					<h4 class="block" ><b>Evaluación y Selección del Proveedor</b></h4>
				<label style="font-size:13px;margin-left:1%;color:grey"><b>Completar los campos a fin de determinar la dimensión del servicio o bien requerido</b>
				</label>
				
				</div>
				<br>
						<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">Macroproceso<span class="required">
							*</span>
							</label>
							<div class="col-md-2 macroproceso">
								<select class="form-control input-large select2me macroproceso" data-placeholder="Select..." name="macro" id="macro" required>
									<option value="" selected></option>

								</select>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">Proceso <span class="required">
							* </span>
							</label>
							<div class="col-md-2 proceso">
								<select class="form-control input-large select2me proceso" data-placeholder="Select..." name="proce" required>
									<option value="" selected></option>
									
								</select>
							</div>
						</div>
					</div>
					
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">¿Procesamiento de datos en el exterior? <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="ext" required>
									<option value="" selected></option>
									<option value="Si">Si</option>
									<option value="No">No</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">¿Contratación Corporativa? <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="corp" required>
									<option value="" selected></option>
									<option value="Si">Si</option>
									<option value="No">No</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">¿Desarrollo de actividades dentro de Prima? <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="dact" required>
									<option value="" selected></option>
									<option value="Si">Si</option>
									<option value="No">No</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">¿Prima es sujeto de Supervisión / Regulación? <span class="required">
							* </span>
							</label>
							<div class="col-md-2">
								<select class="form-control input-small select2me" data-placeholder="Select..." name="supreg" required>
									<option value="" selected></option>
									<option value="Si">Si</option>
									<option value="No">No</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-6">
						<div class="form-group">
							<label class="control-label col-md-5">Tipo de Actividad a Contratar <span class="required">
							* </span>
							</label>
							<div class="col-md-2 tacontratar">
								<select class="form-control input-large select2me tacontratar" data-placeholder="Select..." name="tac" id ="tac" required>
									<option value="" selected></option>
								</select>
							</div>
						</div>
					</div>
					<div class="row">
						
					</div>
					<div class="col-md-12">
					<h4 class="block"  style="text-decoration: underline;">Definición del Impacto</h4>
					</div>

						<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">La interrupción del bien/servicio prestado qué tipo de impacto generaría en la continuidad operativa</label>
							<div class="col-md-2">
								<select class="form-control input-medium select2me" data-placeholder="Select..." name="timp" required>
									<option value="" selected></option>
									<option value="Bajo">Bajo</option>
									<option value="Moderado">Moderado</option>
									<option value="Relevante">Relevante</option>
									<option value="Alto">Alto</option>
									<option value="Crítico">Crítico</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">Qué tipo de información de Prima AFP o sus clientes será administrada por el proveedor</label>
							<div class="col-md-2">
								<select class="form-control input-medium select2me" data-placeholder="Select..." name="info" required>
									<option value="" selected></option>
									<option value="No Aplica">No Aplica</option>
									<option value="Uso Público">Uso Público</option>
									<option value="Uso Interno">Uso Interno</option>
									<option value="Confidencial">Confidencial</option>
								</select>
							</div>
					
					</div>
						</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">La interrupción del bien/servicio prestado podría llevar a un riesgo reputacional de qué nivel</label>
							<div class="col-md-2">
								<select class="form-control input-medium select2me" data-placeholder="Select..." name="rrep" required>
									<option value="" selected></option>
									<option value="Bajo">Bajo</option>
									<option value="Moderado">Moderado</option>
									<option value="Relevante">Relevante</option>
									<option value="Alto">Alto</option>
									<option value="Crítico">Crítico</option>
								</select>
							</div>
						</div>
						</div>
						<div class="row"></div>
						<div class="col-md-12">
							<h4 class="block"  style="text-decoration: underline;">Definición de la Criticidad</h4>
						</div>
					
			
						<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">La cantidad de proveedores en el mercado que pueden brindar el bien/servicio deseado en el mercado</label>
							<div class="col-md-2">
								<select class="form-control input-medium select2me" data-placeholder="Select..." name="cant" required>
									<option value="" selected></option>
									<option value="1 Proveedor">1 Proveedor</option>
									<option value="Hasta 2 Proveedores">Hasta 2 Proveedores</option>
									<option value="Hasta 3 Proveedores">Hasta 3 Proveedores</option>
									<option value="Hasta 4 Proveedores">Hasta 4 Proveedores</option>
									<option value="Más de 4 Proveedores">Más de 4 Proveedores</option>
									
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">El cambiar de proveedor qué nivel de impacto negativo podría generar en Prima AFP</label>
							<div class="col-md-2">
								<select class="form-control input-medium select2me" data-placeholder="Select..." name="impn" required>
									<option value="" selected></option>
									<option value="Ningún Impacto">Ningún Impacto</option>
									<option value="Bajo Impacto">Bajo Impacto</option>
									<option value="Mediano Impacto">Mediano Impacto</option>
									<option value="Alto Impacto">Alto Impacto</option>
								</select>
							</div>
						</div>
					</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-6">La relación del bien o servicio a contratar será de  ...</label>
							<div class="col-md-2">
								<select class="form-control input-medium select2me" data-placeholder="Select..." name="rela">
									<option value="" selected></option>
									<option value="Única vez">Única vez</option>
									<option value="Corto Plazo">Corto Plazo</option>
									<option value="Mediano Plazo">Mediano Plazo</option>
									<option value="Largo Plazo">Largo Plazo</option>
								</select>
							</div>
						</div>
					</div>
					<div class="row">
					<div class="col-md-offset-6 col-md-8">
						<input type="submit" name="reg2" id="reg2" position="center" class="btn btn-success" value="Registrar"> 	
					</div>
					</div>
				</form>
				<label style="color:red;">&nbsp;Todos los campos son de caracter obligatorio</label>	

				<div class="form-actions">
					<div class="row-a">
						<div class="col-md-1" style="display:block;" id="atras1">
							<a href="javascript:;" class="btn blue button-previous">
							<i class="m-icon-swapleft m-icon-white"></i></a>
						</div>
						<div class="col-md-1" style="display:none" id="siguiente1">				
							<a href="javascript:;" class="btn green button-next" >
							<i class="m-icon-swapright m-icon-white"></i>
							</a>
						</div>
						<div class="col-md-offset-1 col-md-9" style="display:none" id="fin1">
							<a href="javascript:;" class="btn yellow button-submit" id="fin">
							Finalizar <i class="m-icon-swapright m-icon-white"></i>  
							</a>
							
						</div>
					</div>
				</div>

	<?php
	}
	mysqli_free_result($resultado2);
	mysqli_free_result($resultado3);
	?>
	</div>

	<div class="tab-pane" id="tab3">
		<div class="portlet-body" style="display:none;">
							<div class="row">
								<div class="col-md-3">
									<div class="form-group">
										<label class="control-label" for="title">Title</label>
										<input id="title" type="text" class="form-control" value="Mensaje" placeholder="Enter a title ..."/>
									</div>
									<div class="form-group">
										<label class="control-label" for="message">Message</label>
										<textarea class="form-control" id="message" rows="3" placeholder="">Adjuto agregado correctamente</textarea>
									</div>
									<div class="form-group">
										<div class="checkbox-list">
											<label for="closeButton">
											<input id="closeButton" type="checkbox" value="checked" checked class="input-small"/>Close Button </label>
											<label for="addBehaviorOnToastClick">
											<input id="addBehaviorOnToastClick" type="checkbox" value="checked" class="input-small"/>Add behavior on toast click </label>
											<label for="debugInfo">
											<input id="debugInfo" type="checkbox" value="checked" class="input-small"/>Debug </label>
										</div>
									</div>
								</div>
								<div class="col-md-3">
									<div class="form-group" id="toastTypeGroup">
										<label>Toast Type</label>
										<div class="radio-list">
											<label>
											<input type="radio" name="toasts" value="success" checked/>Success </label>
											<label>
											<input type="radio" name="toasts" value="info"/>Info </label>
											<label>
											<input type="radio" name="toasts" value="warning"/>Warning </label>
											<label>
											<input type="radio" name="toasts" value="error"/>Error </label>
										</div>
									</div>
									<div class="form-group" id="positionGroup">
										<label>Position</label>
										<div class="radio-list">
											<label>
											<input type="radio" name="positions" value="toast-top-right"/>Top Right </label>
											<label>
											<input type="radio" name="positions" value="toast-bottom-right" checked/>Bottom Right </label>
											<label>
											<input type="radio" name="positions" value="toast-bottom-left"/>Bottom Left </label>
											<label>
											<input type="radio" name="positions" value="toast-top-left"/>Top Left </label>
											<label>
											<input type="radio" name="positions" value="toast-top-center"/>Top Center </label>
											<label>
											<input type="radio" name="positions" value="toast-bottom-center"/>Bottom Center </label>
											<label>
											<input type="radio" name="positions" value="toast-top-full-width"/>Top Full Width </label>
											<label>
											<input type="radio" name="positions" value="toast-bottom-full-width"/>Bottom Full Width </label>
										</div>
									</div>
								</div>
								<div class="col-md-3">
									<div class="form-group">
										<div class="controls">
											<label class="control-label" for="showEasing">Show Easing</label>
											<input id="showEasing" type="text" placeholder="swing, linear" class="form-control input-small" value="swing"/>
											<label class="control-label" for="hideEasing">Hide Easing</label>
											<input id="hideEasing" type="text" placeholder="swing, linear" class="form-control input-small" value="linear"/>
											<label class="control-label" for="showMethod">Show Method</label>
											<input id="showMethod" type="text" placeholder="show, fadeIn, slideDown" class="form-control input-small" value="fadeIn"/>
											<label class="control-label" for="hideMethod">Hide Method</label>
											<input id="hideMethod" type="text" placeholder="hide, fadeOut, slideUp" class="form-control input-small" value="fadeOut"/>
										</div>
									</div>
								</div>
								<div class="col-md-3">
									<div class="form-group">
										<div class="controls">
											<label class="control-label" for="showDuration">Show Duration</label>
											<input id="showDuration" type="text" placeholder="ms" class="form-control input-small" value="1000"/>
											<label class="control-label" for="hideDuration">Hide Duration</label>
											<input id="hideDuration" type="text" placeholder="ms" class="form-control input-small" value="1000"/>
											<label class="control-label" for="timeOut">Time out</label>
											<input id="timeOut" type="text" placeholder="ms" class="form-control input-small" value="5000"/>
											<label class="control-label" for="timeOut">Extended time out</label>
											<input id="extendedTimeOut" type="text" placeholder="ms" class="form-control input-small" value="1000"/>
										</div>
									</div>
								</div>
							</div>
							
							<div class="row margin-top-10">
								<div class="col-md-12">
									<pre id='toastrOptions'>
										 Settings...
									</pre>
								</div>
							</div>
		</div>
	<div style="display:none;" id="operaciones" >

		<?php  while($rowst = mysqli_fetch_array($resultadost,MYSQLI_ASSOC))
    	{
    	?>
		<div id="suma1">
			<input type="number" name="sum1" class="stotal" id="sum1" value="<?php echo ($rowst['st1'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum2" class="stotal" id="sum2" value="<?php echo ($rowst['st2'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum3" class="stotal" id="sum3" value="<?php echo ($rowst['st3'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum4" class="stotal" id="sum4" value="<?php echo ($rowst['st4'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum5" class="stotal" id="sum5" value="<?php echo ($rowst['st5'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum6" class="stotal" id="sum6" value="<?php echo ($rowst['st6'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum7" class="stotal" id="sum7" value="<?php echo ($rowst['st7'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum8" class="stotal" id="sum8" value="<?php echo ($rowst['st8'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum9" class="stotal" id="sum9" value="<?php echo ($rowst['st9'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum10" class="stotal" id="sum10" value="<?php echo ($rowst['st10'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum11" class="stotal" id="sum11" value="<?php echo ($_SESSION['cp1'] * $_SESSION['economico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
		</div>
		<?php }

		while($rowst1 = mysqli_fetch_array($resultadost1,MYSQLI_ASSOC))
    	{
    		?>
    	<div  id="suma2">
			<input type="number" name="sum1" class="stotal1" id="sum1" value="<?php echo ($rowst1['st1'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum2" class="stotal1" id="sum2" value="<?php echo ($rowst1['st2'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum3" class="stotal1" id="sum3" value="<?php echo ($rowst1['st3'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum4" class="stotal1" id="sum4" value="<?php echo ($rowst1['st4'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum5" class="stotal1" id="sum5" value="<?php echo ($rowst1['st5'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum6" class="stotal1" id="sum6" value="<?php echo ($rowst1['st6'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum7" class="stotal1" id="sum7" value="<?php echo ($rowst1['st7'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum8" class="stotal1" id="sum8" value="<?php echo ($rowst1['st8'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum9" class="stotal1" id="sum9" value="<?php echo ($rowst1['st9'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum10" class="stotal1" id="sum10" value="<?php echo ($rowst1['st10'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum11" class="stotal1" id="sum11" value="<?php echo ($_SESSION['cp2'] * $_SESSION['economico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
	</div>
	<?php }

		while($rowst2 = mysqli_fetch_array($resultadost2,MYSQLI_ASSOC))
    	{
    		?>
    <div id="suma3">
			<input type="number" name="sum1" class="stotal2" id="sum1" value="<?php echo ($rowst2['st1'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum2" class="stotal2" id="sum2" value="<?php echo ($rowst2['st2'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum3" class="stotal2" id="sum3" value="<?php echo ($rowst2['st3'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum4" class="stotal2" id="sum4" value="<?php echo ($rowst2['st4'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum5" class="stotal2" id="sum5" value="<?php echo ($rowst2['st5'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum6" class="stotal2" id="sum6" value="<?php echo ($rowst2['st6'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum7" class="stotal2" id="sum7" value="<?php echo ($rowst2['st7'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum8" class="stotal2" id="sum8" value="<?php echo ($rowst2['st8'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum9" class="stotal2" id="sum9" value="<?php echo ($rowst2['st9'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum10" class="stotal2" id="sum10" value="<?php echo ($rowst2['st10'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum11" class="stotal2" id="sum11" value="<?php echo ($_SESSION['cp3'] * $_SESSION['economico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
 	</div>
 	<?php }

		while($rowst3 = mysqli_fetch_array($resultadost3,MYSQLI_ASSOC))
    	{
    		?>
    <div id="suma4">
			<input type="number" name="sum1" class="stotal3" id="sum1" value="<?php echo ($rowst3['st1'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum2" class="stotal3" id="sum2" value="<?php echo ($rowst3['st2'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum3" class="stotal3" id="sum3" value="<?php echo ($rowst3['st3'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum4" class="stotal3" id="sum4" value="<?php echo ($rowst3['st4'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum5" class="stotal3" id="sum5" value="<?php echo ($rowst3['st5'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum6" class="stotal3" id="sum6" value="<?php echo ($rowst3['st6'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum7" class="stotal3" id="sum7" value="<?php echo ($rowst3['st7'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum8" class="stotal3" id="sum8" value="<?php echo ($rowst3['st8'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum9" class="stotal3" id="sum9" value="<?php echo ($rowst3['st9'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum10" class="stotal3" id="sum10" value="<?php echo ($rowst3['st10'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum11" class="stotal3" id="sum11" value="<?php echo ($_SESSION['cp4'] * $_SESSION['economico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
	</div>
	<?php }

		while($rowst4 = mysqli_fetch_array($resultadost4,MYSQLI_ASSOC))
    	{
    		?>
    <div  id="suma5">
			<input type="number" name="sum1" class="stotal4" id="sum1" value="<?php echo ($rowst4['st1'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum2" class="stotal4" id="sum2" value="<?php echo ($rowst4['st2'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum3" class="stotal4" id="sum3" value="<?php echo ($rowst4['st3'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum4" class="stotal4" id="sum4" value="<?php echo ($rowst4['st4'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum5" class="stotal4" id="sum5" value="<?php echo ($rowst4['st5'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum6" class="stotal4" id="sum6" value="<?php echo ($rowst4['st6'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum7" class="stotal4" id="sum7" value="<?php echo ($rowst4['st7'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum8" class="stotal4" id="sum8" value="<?php echo ($rowst4['st8'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum9" class="stotal4" id="sum9" value="<?php echo ($rowst4['st9'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum10" class="stotal4" id="sum10" value="<?php echo ($rowst4['st10'] * $_SESSION['tecnico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
            <input type="number" name="sum11" class="stotal4" id="sum11" value="<?php echo ($_SESSION['cp5'] * $_SESSION['economico']);?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
 	</div>
 	<?php }?>
</div>

		<?php 
		while($rows = mysqli_fetch_array($resultado5,MYSQLI_ASSOC) and $row = mysqli_fetch_array($resultado4,MYSQLI_ASSOC)){
				{
				if($rows['acepsel']==""){ 

		?>		
				<div id="criterios" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="40%">
					<form method="POST" id="critform1">
						<div class="modal-header">
							<button type="button" class="close" data-dismiss="modal" aria-hidden="true"></button>
							<h4 class="modal-title">Matriz de Criterios para la Evaluación de Proveedores</h4>
						</div>
						<div class="modal-body">

							<fieldset>
								<label><b>Criterios Globales de Elección</b></label>
								<br>
								<input type="text" name="anuncio" id="anuncio" value="La suma de Porcentajes debe ser 100" class="form-control input-slarge" style="border:none;text-align:center;font-size:12px;color:orange;font-weight: bold;">
								<div class="col-md-12">
								<div class="col-md-6">
								<label style="margin-left:20%;">Evaluación Económica (%):</label><input type="number" min="40" max="99" value="<?php if($_SESSION['teconomico'] > 0) { echo $_SESSION['teconomico']; }else{ echo 40;} ?>" name="peconomico" id="peconomico" class="form-control input-xsmall" onchange="comprobar()" style="margin-left: 35%;text-align:center;" />	
								</div>
								<div class="col-md-6">
								<label style="margin-left:20%;">Evaluación Técnica (%):</label><input type="number" name="ptecnico" value="<?php if($_SESSION['etecnico'] > 0) { echo $_SESSION['etecnico']; }else{ echo 60;} ?>" id="ptecnico" class="form-control input-xsmall" onchange="comprobar2()" style="margin-left: 30%;text-align:center;">
								<br>
								</div>
								</div>
								<br>

							</fieldset>
							<fieldset>
								<label><b>Evaluación Económica (S/.)</b> </label><label style="font-size:12px;"> - Por favor coloque el monto cotizado por cada proveedor</label>
								<br>
								<div class="col-md-12">
								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Proveedor 1:</label></div>
									<div class="col-md-4"><input type="number"  name="ppro1" id="ppro1" class="form-control input-small" value="<?php if($_SESSION['ccp1'] > 0) { echo $_SESSION['ccp1']; }else{ echo 0;} ?>" style="text-align:center;" />	</div>
								</div>
								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Proveedor 2:</label></div>
									<div class="col-md-4"><input type="number"   name="ppro2" id="ppro2" class="form-control input-small" value="<?php if($_SESSION['ccp2'] > 0) { echo $_SESSION['ccp2']; }else{ echo 0;} ?>" style="text-align:center;" />		</div>
								</div>
								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Proveedor 3:</label></div>
									<div class="col-md-4"><input type="number"  name="ppro3" id="ppro3" class="form-control input-small" value="<?php if($_SESSION['ccp3'] > 0) { echo $_SESSION['ccp3']; }else{ echo 0;} ?>" style="text-align:center;" />	</div>		
								</div>

								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Proveedor 4:</label></div>
									<div class="col-md-4"><input type="number"   name="ppro4" id="ppro4" class="form-control input-small" value="<?php if($_SESSION['ccp4'] > 0) { echo $_SESSION['ccp4']; }else{ echo 0;} ?>" style="text-align:center;" />	</div>		
								</div>
								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Proveedor 5:</label></div>
									<div class="col-md-4"><input type="number"  name="ppro5" id="ppro5" class="form-control input-small" value="<?php if($_SESSION['ccp5'] > 0) { echo $_SESSION['ccp5']; }else{ echo 0;} ?>" style="text-align:center;" />	</div>
								</div>
								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Valor Minimo:</label></div>
									<div class="col-md-4"><input type="number"  name="pminimo" id="pminimo" class="form-control input-small" value="<?php if($_SESSION['cpm'] > 0) { echo $_SESSION['cpm']; }else{ echo 0;} ?>" style="text-align:center;" readonly/>	</div>
								</div>
								<br>
								</div>
								<br>

							</fieldset>
							<fieldset>
								<br>
								      <label><b>Evaluación Técnica</b> </label>
								      <br>
								      <!-- <input type="button" id="btnAdd" value="+" class="btn green" />
								      <input type="button" id="btnDel" value="-" class="btn red"/> -->
								     <label style="color: red; padding-left: 50%;"><b>TOTAL: <input type="number" name="pesos" id="pesos" style="width: 40px;border:none;background-color:white;" value="" disabled></b><b>%</b></label>
							</fieldset>	
							<div class="col-md-5">
									<p>
									<label>Criterios</label>
									</p>
								      <?php
										while($rowc = mysqli_fetch_array($resultadoc,MYSQLI_ASSOC))
											{
											if($rowc['cri10']!=""){?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input7" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name7" id="name7" value="<?php echo $rowc['cri7'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input8" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name8" id="name8" value="<?php echo $rowc['cri8'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input9" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name9" id="name9" value="<?php echo $rowc['cri9'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input10" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name10" id="name10" value="<?php echo $rowc['cri10'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php
											}elseif ($rowc['cri9']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input7" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name7" id="name7" value="<?php echo $rowc['cri7'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input8" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name8" id="name8" value="<?php echo $rowc['cri8'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input9" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name9" id="name9" value="<?php echo $rowc['cri9'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php	
											} elseif ($rowc['cri8']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input7" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name7" id="name7" value="<?php echo $rowc['cri7'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input8" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name8" id="name8" value="<?php echo $rowc['cri8'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php	
											} elseif ($rowc['cri7']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input7" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name7" id="name7" value="<?php echo $rowc['cri7'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php		
											} elseif ($rowc['cri6']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php							
											} elseif ($rowc['cri5']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php						
											} elseif ($rowc['cri4']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php					
											} elseif ($rowc['cri3']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php
											} elseif ($rowc['cri2']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php	
											} elseif ($rowc['cri1']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php	
											}else{?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php	
											} 
										}?>
										<fieldset>
											<input type="button" id="btnAdd" value="+ Agregar" class="btn green" />
								      		<input type="button" id="btnDel" value="- Quitar" class="btn red"/>
								  		</fieldset>
									  
							</div>

							<div class="col-md-6" style="left: 40px;">
								<p>
									<label>Peso (%) </label>
								</p>
								<?php
										while($rowcr = mysqli_fetch_array($resultadocr,MYSQLI_ASSOC) and $rowp = mysqli_fetch_array($resultadop,MYSQLI_ASSOC))
											{
											if($rowcr['cri10']!=""){?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" class="inputs" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out7" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape7" class="inputs" id="ape7" value="<?php echo $rowp['pcri7'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out8" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape8" class="inputs" id="ape8" value="<?php echo $rowp['pcri8'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out9" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape9" class="inputs" id="ape9" value="<?php echo $rowp['pcri9'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out10" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape10" class="inputs" id="ape10" value="<?php echo $rowp['pcri10'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php
											}elseif ($rowcr['cri9']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" class="inputs" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out7" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape7" class="inputs" id="ape7" value="<?php echo $rowp['pcri7'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out8" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape8" class="inputs" id="ape8" value="<?php echo $rowp['pcri8'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out9" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape9" class="inputs" id="ape9" value="<?php echo $rowp['pcri9'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php	
											} elseif ($rowcr['cri8']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" class="inputs" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out7" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape7" class="inputs" id="ape7" value="<?php echo $rowp['pcri7'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out8" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape8" class="inputs" id="ape8" value="<?php echo $rowp['pcri8'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php	
											} elseif ($rowcr['cri7']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" class="inputs" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out7" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape7" class="inputs" id="ape7" value="<?php echo $rowp['pcri7'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php		
											} elseif ($rowcr['cri6']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" class="inputs" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php							
											} elseif ($rowcr['cri5']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php						
											} elseif ($rowcr['cri4']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php					
											} elseif ($rowcr['cri3']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php
											} elseif ($rowcr['cri2']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php	
											} elseif ($rowcr['cri1']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php	
											}else{?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php	
											} 
										}
										 
										  ?>
							</div>
						</div>

						<div class="modal-footer">
							<button type="submit" position="center" class="btn btn-success" id="registrar" name="registrar">Registrar</button>
							<button type="button" data-dismiss="modal" class="btn btn-default">Cerrar</button>
						</div>

				</form>
			</div>

			<div id="valor" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="420">
				<form method="POST" id="valorform">
						<div class="modal-header">
							<button type="button" class="close" data-dismiss="modal" aria-hidden="true"></button>
							<h4 class="modal-title">Valorar Criterios</h4>
						</div>

						<div class="modal-body" id ="valorado">
								
						</div>

						<div class="modal-footer">
							<button type="submit" name="valorar" id="valorar" position="center" class="btn btn-success">Valorar</button>
							<button type="button" data-dismiss="modal" class="btn btn-default">Cerrar</button>
						</div>

						<input type="text" name="idp" id="idp" style="width: 50px; height: 30px;display:none"/>
						<input type="text" name="tmp" id="tmp" style="width: 50px; height: 30px;display:none"/>
						<input type="text" name="tprov" id="tprov" style="width: 50px; height: 30px;display:none"/>

				</form>
			</div>
				<form method="POST" id="formtab3" action="insert3.php">	
					<div class="col-md-12">
						<h4 class="block col-md-6"><b>Evaluación y Seleccion del Proveedor</b></h4>
					</div>
					<label style="color:gray;margin-left:1%;">
						1.- Agregar los criterios para evaluar a los proveedores elegidos → <a class="btn default" data-toggle="modal" href="#criterios"  id="elcrit" name="elcrit">
					Agregar Criterios</a><br>
						2.- Seleccionar a los proveedores que participaran del concurso de no figurar en la lista crearlo aqui → <a class="btn default" data-toggle="modal" href="#provve"  id="provv" name="provv">
					Agregar Proveedor</a><br>
						3.- Subir Cotización de cada proveedor elegido<br>
						4.- Evaluar a cada proveedor según los criterios definidos<br>
						5.- De estar conforme con la sugerencia registrar la información, caso contrario, elegir a otro proveedor y justificar el porque de su elección<br>
					</label>

					<div class="col-md-12">
						<h4 class="block col-md-6"><b>Proveedor</b></h4>
					</div>
					<?php

					while($mando = mysqli_fetch_array($tblmando1,MYSQLI_ASSOC))
					{
					if($mando['cotizaciones'] == 3){

					?>
					<div class="col-md-12">
						<div class="form-group">	
							<label class="control-label col-md-1" style="margin-left:3%;">1<span class="required">
							* </span>
							</label>
							
							<span class="btn blue fileinput-button" style="left: -4%;">
								<i class="fa fa-file" id="control" name="control"></i> Subir Cotización
								<input type="file" id="cot" name="cot" required>
							</span>
							<b><span class="col-md-1" type="number" name="total"  id="total" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: -3%;" data-toggle="modal" href="#valor" id="evaluador" name="evaluador"> Evaluar </a>
							<div class="col-md-3 proveedor1" style="left: -9%;">
								<select class="form-control input-xlarge select2me proveedor1" data-placeholder="Select..." name="p1" id="p1" required>
									<option value=""></option>
								</select>
								
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1" style="margin-left:3%;">2<span class="required">
							* </span>
							</label>

							<span class="btn blue fileinput-button" style="left: -4%;">
								<i class="fa fa-file" id="control1" name="control1"></i> Subir Cotización
								<input type="file" id="cot1" name="cot1" required>
							</span>

							<b><span class="col-md-1" type="number" name="total1"  id="total1" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: -3%;" data-toggle="modal" href="#valor" id="evaluador1" name="evaluador1"> Evaluar </a>
							<div class="col-md-3 proveedor2" style="left: -9%;">
								<select class="form-control input-xlarge select2me proveedor2" data-placeholder="Select..." name="p2" id="p2" required>
								
								</select>
								
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1" style="margin-left:3%;">3<span class="required">
							* </span>
							</label>

							<span class="btn blue fileinput-button" style="left: -4%;">
								<i class="fa fa-file" id="control2" name="control2"></i> Subir Cotización
								<input type="file" id="cot2" name="cot2" required>
							</span>
							
							<b><span class="col-md-1" type="number" name="total2"  id="total2" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: -3%;" data-toggle="modal" href="#valor" id="evaluador2" name="evaluador2"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -9%;">	
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p3" id="p3" required>
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1" style="margin-left:3%;">4</label>

							<span class="btn blue fileinput-button" style="left: -4%;">
								<i class="fa fa-file" id="control3" name="control3"></i> Subir Cotización
								<input type="file" id="cot3" name="cot3">
							</span>
							
							<b><span class="col-md-1" type="number" name="total3"  id="total3" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: -3%;" data-toggle="modal" href="#valor" id="evaluador3" name="evaluador3"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -9%;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p4" id="p4">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1" style="margin-left:3%;">5</label>
							
							<span class="btn blue fileinput-button" style="left: -4%;">
								<i class="fa fa-file" id="control4" name="control4"></i> Subir Cotización
								<input type="file" id="cot4" name="cot4">
							</span>

							<b><span class="col-md-1" type="number" name="total4"  id="total4" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: -3%;" data-toggle="modal" href="#valor" id="evaluador4" name="evaluador4"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -9%;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p5" id="p5">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>
					<?php
				}
				if ($mando['cotizaciones'] == 2)
				{

				?>
				<div class="col-md-12">
						<div class="form-group">	
							<label class="control-label col-md-1" style="margin-left:3%;">1<span class="required">
							* </span>
							</label>
							
							<span class="btn blue fileinput-button" style="left: -4%;">
								<i class="fa fa-file" id="control" name="control"></i> Subir Cotización
								<input type="file" id="cot" name="cot" required>
							</span>

							<b><span class="col-md-1" type="number" name="total"  id="total" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: -3%;" data-toggle="modal" href="#valor" id="evaluador" name="evaluador"> Evaluar </a>
							<div class="col-md-3 proveedor1" style="left: -9%;">
								<select class="form-control input-xlarge select2me proveedor1" data-placeholder="Select..." name="p1" id="p1" required>
									<option value=""></option>
								</select>
								
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1" style="margin-left:3%;">2<span class="required">
							* </span>
							</label>

							<span class="btn blue fileinput-button" style="left: -4%;">
								<i class="fa fa-file" id="control1" name="control1"></i> Subir Cotización
								<input type="file" id="cot1" name="cot1" required>
							</span>

							<b><span class="col-md-1" type="number" name="total1"  id="total1" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: -3%;" data-toggle="modal" href="#valor" id="evaluador1" name="evaluador1"> Evaluar </a>
							<div class="col-md-3 proveedor2" style="left: -9%;">
								<select class="form-control input-xlarge select2me proveedor2" data-placeholder="Select..." name="p2" id="p2" required>
								
								</select>
								
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1" style="margin-left:3%;">3
							</label>

							<span class="btn blue fileinput-button" style="left: -4%;">
								<i class="fa fa-file" id="control2" name="control2"></i> Subir Cotización
								<input type="file" id="cot2" name="cot2">
							</span>
							
							<b><span class="col-md-1" type="number" name="total2"  id="total2" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: -3%;" data-toggle="modal" href="#valor" id="evaluador2" name="evaluador2"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -9%;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p3" id="p3">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1" style="margin-left:3%;">4
							</label>

							<span class="btn blue fileinput-button" style="left: -4%;">
								<i class="fa fa-file" id="control3" name="control3"></i> Subir Cotización
								<input type="file" id="cot3" name="cot3">
							</span>
							
							<b><span class="col-md-1" type="number" name="total3"  id="total3" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: -3%;" data-toggle="modal" href="#valor" id="evaluador3" name="evaluador3"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -9%;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p4" id="p4">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1" style="margin-left:3%;">5
							</label>
							
							<span class="btn blue fileinput-button" style="left: -4%;">
								<i class="fa fa-file" id="control4" name="control4"></i> Subir Cotización
								<input type="file" id="cot4" name="cot4">
							</span>

							<b><span class="col-md-1" type="number" name="total4"  id="total4" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: -3%;" data-toggle="modal" href="#valor" id="evaluador4" name="evaluador4"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -9%;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p5" id="p5">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>
				<?php
				}
				if ($mando['cotizaciones'] == 1)
				{

				?>
				<div class="col-md-12">
						<div class="form-group">	
							<label class="control-label col-md-1" style="margin-left:3%;">1<span class="required">
							* </span>
							</label>
							
							<span class="btn blue fileinput-button" style="left: -4%;">
								<i class="fa fa-file" id="control" name="control"></i> Subir Cotización
								<input type="file" id="cot" name="cot" required>
							</span>

							<b><span class="col-md-1" type="number" name="total"  id="total" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: -3%;" data-toggle="modal" href="#valor" id="evaluador" name="evaluador"> Evaluar </a>
							<div class="col-md-3 proveedor1" style="left: -9%;">
								<select class="form-control input-xlarge select2me proveedor1" data-placeholder="Select..." name="p1" id="p1" required>
									<option value=""></option>
								</select>
								
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1" style="margin-left:3%;">2
							</label>

							<span class="btn blue fileinput-button" style="left: -4%;">
								<i class="fa fa-file" id="control1" name="control1"></i> Subir Cotización
								<input type="file" id="cot1" name="cot1">
							</span>


							<b><span class="col-md-1" type="number" name="total1"  id="total1" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: -3%;" data-toggle="modal" href="#valor" id="evaluador1" name="evaluador1"> Evaluar </a>
							<div class="col-md-3 proveedor2" style="left: -9%;">
								<select class="form-control input-xlarge select2me proveedor2" data-placeholder="Select..." name="p2" id="p2">
								
								</select>
								
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1"style="margin-left:3%;">3
							</label>

							<span class="btn blue fileinput-button" style="left: -4%;">
								<i class="fa fa-file" id="control2" name="control2"></i> Subir Cotización
								<input type="file" id="cot2" name="cot2">
							</span>
							
							<b><span class="col-md-1" type="number" name="total2"  id="total2" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: -3%;" data-toggle="modal" href="#valor" id="evaluador2" name="evaluador2"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -9%;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p3" id="p3">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1" style="margin-left:3%;">4</label>

							<span class="btn blue fileinput-button" style="left: -4%;">
								<i class="fa fa-file" id="control3" name="control3"></i> Subir Cotización
								<input type="file" id="cot3" name="cot3">
							</span>
							
							<b><span class="col-md-1" type="number" name="total3"  id="total3" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: -3%;" data-toggle="modal" href="#valor" id="evaluador3" name="evaluador3"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -9%;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p4" id="p4">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1" style="margin-left:3%;">5</label>
							
							<span class="btn blue fileinput-button" style="left: -4%;">
								<i class="fa fa-file" id="control4" name="control4"></i> Subir Cotización
								<input type="file" id="cot4" name="cot4">
							</span>

							<b><span class="col-md-1" type="number" name="total4"  id="total4" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: -3%;" data-toggle="modal" href="#valor" id="evaluador4" name="evaluador4"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -9%;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p5" id="p5">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>
					
					<?php
					}
				}
					?>


					<div id="responsive" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="380">
						<div class="modal-header">
							<button type="button" class="close" data-dismiss="modal" aria-hidden="true"></button>
							<h4 class="modal-title">Nuevo Proveedor</h4>
						</div>
						<div class="modal-body">
							<div class="row">
								<div class="col-md-12">
									<h4></h4>
									<p>
										<label>Nombre del Proveedor</label>
										<input class="form-control" type="text">
									</p>
									<p>
										<label>RUC</label>	
										<input class="form-control" type="text">
									</p>
									<p>
										<label>Dirección</label>
										<input class="form-control" type="text">
									</p>
									<p>
										<label>Persona de Contacto</label>
										<input class="form-control" type="text">
									</p>
									<p>
										<label>Teléfono</label>
										<input class="form-control" type="text">
									</p>
								</div>
							</div>
						</div>
						<div class="modal-footer">
							<button type="button" data-dismiss="modal" class="btn btn-default">Close</button>
							<button type="button" class="btn blue">Save changes</button>
						</div>
					</div>
					
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-2">Sugerido para Contratar<span class="required">
							* </span>
							</label>
							<div class="col-md-1 proveedore" style="left:-4%;">
								<input type="text" style="text-align: center" class="form-control input-xlarge select2me proveedor" name="ps" id="ps" value="" readonly/>
							</div>

							<div class="col-md-3" style="left:18%;padding-top:-8%;">
								<input type="checkbox" style="text-align: center; " onclick="captar();" class="md-check" name="psug" id="psug"/><label>&nbsp;Elegir Otro Proveedor</label>
							</div>

							<div class="col-md-1 proveedor" style="left:5%;">	
								<select type = "text" style="text-align: center" class="form-control input-xlarge select2me proveedor" data-placeholder="Select..." name="pe" id="pe" disabled>
									<option value=""></option>
								</select >	
							</div>
						</div>
						<input type="text" name="pelegido" id="pelegido" style="display:none;">
						<input type="text" name="cote" id="cote" style="display:none;">
						<input type="text" name="cote1" id="cote1" style="display:none;">
						<input type="text" name="cote2" id="cote2" style="display:none;">
						<input type="text" name="cote3" id="cote3" style="display:none;">
						<input type="text" name="cote4" id="cote4" style="display:none;">
					</div>

					<div class="col-md-12">
						<div class="form-group" style="text-align:center;">
							<div class="col-md-3" style="left:80px;top:30px;">
								<label>Sustento del cambio <span class="required" style="color:red">
							* </span> </label>
							</div>
							<textarea placeholder="Comentario..." id="comentotro" name="comentotro" class="form-control" style="margin: 0px;width: 706px;height: 86px;" readonly="readonly"></textarea>
						</div>
						<label style="color:red;">&nbsp;Los campos que contengan <b>(*)</b> Son de caracter obligatorio</label>
					</div>
					
				<div class="row" name="gistro" id="gistro" style="display:block;">
					<div class="col-md-offset-5 col-md-8">
						<input type="submit"  position="center" class="btn btn-success" value="Registrar"> 	
					</div>
				</div>
			</form>
			<div id="provve" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="420">
					<div class="modal-header">
							<button type="button" class="close" data-dismiss="modal" aria-hidden="true"></button>
							<h4 class="modal-title">Agregar Proveedor</h4>
						</div>

						<div class="modal-body">
							<form method="POST" id="provform">
								<input type="text" name="controlproveedor" id="controlproveedor" style="display:none;" value="vacio">
                                    <div class="form-group form-md-line-input">
                                        <label class="col-md-5 control-label">Nombre Proveedor:</label>
                                        <div class="col-md-7">
                                            <input type="text" class="form-control" id="nruc" name="nruc" placeholder="Nombre" style="font-size:14px;margin-top:-6px;" required>
                                            <div class="form-control-focus"> </div>
                                        </div>
                                    </div>
                                    <div class="form-group form-md-line-input">
                                        <label  class="col-md-5 control-label">RUC:</label>
                                        <div class="col-md-7">
                                            <input type="number" class="form-control" id="ruc" placeholder="RUC" name ="ruc" style="font-size:14px;margin-top:-6px;" maxlength="11" oninput="if(this.value.length > this.maxLength) this.value = this.value.slice(0, this.maxLength);" required>
                                            <div class="form-control-focus"> </div>
                                        </div>
                                    </div>
                                    
                                    <div class="form-group col-md-12" style="padding-top:15px;">
                                        <div class="col-md-offset-4 col-md-10">
                                            <input type="submit" class="btn blue" value="Agregar" id="menprov" name="menprov">
                                        </div>
                                    </div>
                            </form>         
						</div>
				</div>

			<div class="form-actions">
				<div class="row-a">
					<div class="col-md-1" style="display:block;" id="atras2">
						<a href="javascript:;" class="btn blue button-previous" id="atras">
						<i class="m-icon-swapleft m-icon-white"></i></a>
					</div>
					<div class="col-md-1" style="display:none" id="siguiente2">				
						<a href="javascript:;" class="btn green button-next" id="siguiente">
						<i class="m-icon-swapright m-icon-white"></i>
						</a>
					</div>
					<div class="col-md-offset-1 col-md-9" style="display:none" id="fin2">
						<a href="javascript:;" class="btn yellow button-submit" id="fin">
						Finalizar <i class="m-icon-swapright m-icon-white"></i>  
						</a>
						
					</div>
				</div>
			</div>
			<?php
			}else if($rows['acepsel']=='no'){
			?>
			<div id="valoraciones" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="420">
				<form method="POST" id="critform">
						<div class="modal-header">
							<button type="button" class="close" data-dismiss="modal" aria-hidden="true"></button>
							<h4 class="modal-title">Elegir Criterios</h4>
						</div>

						<div class="modal-body">
							<fieldset>
								   	<p>
								      <label></label>
								      <input type="button" id="btnAdd1" value="+" class="btn green" />
								      <input type="button" id="btnDel1" value="-" class="btn red" />
								      <label style="color: red; padding-left: 160px;"><b>TOTAL: <input type="number" name="pesos" id="pesos" style="width: 40px;border:none;background-color:white;" value="100" disabled></b><b>%</b></label>
								  	</p>
							</fieldset>
							<div class="col-md-7">
									<p>
									<label>Criterios</label>
									</p>
								      <?php
										while($rowc = mysqli_fetch_array($resultadoc,MYSQLI_ASSOC))
											{
											if($rowc['cri10']!=""){?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input7" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name7" id="name7" value="<?php echo $rowc['cri7'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input8" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name8" id="name8" value="<?php echo $rowc['cri8'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input9" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name9" id="name9" value="<?php echo $rowc['cri9'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input10" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name10" id="name10" value="<?php echo $rowc['cri10'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php
											}elseif ($rowc['cri9']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input7" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name7" id="name7" value="<?php echo $rowc['cri7'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input8" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name8" id="name8" value="<?php echo $rowc['cri8'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input9" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name9" id="name9" value="<?php echo $rowc['cri9'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php	
											} elseif ($rowc['cri8']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input7" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name7" id="name7" value="<?php echo $rowc['cri7'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input8" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name8" id="name8" value="<?php echo $rowc['cri8'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php	
											} elseif ($rowc['cri7']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input7" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name7" id="name7" value="<?php echo $rowc['cri7'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php		
											} elseif ($rowc['cri6']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php							
											} elseif ($rowc['cri5']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php						
											} elseif ($rowc['cri4']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php					
											} elseif ($rowc['cri3']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php
											} elseif ($rowc['cri2']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php	
											} elseif ($rowc['cri1']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php	
											}else{?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php	
											} 
										}?>
							</div>

							<div class="col-md-5" style="left: 40px;">
								<p>
									<label>Peso (%) </label>
								</p>
								<?php
										while($rowcr = mysqli_fetch_array($resultadocr,MYSQLI_ASSOC) and $rowp = mysqli_fetch_array($resultadop,MYSQLI_ASSOC))
											{
											if($rowcr['cri10']!=""){?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" class="inputs" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out7" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape7" class="inputs" id="ape7" value="<?php echo $rowp['pcri7'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out8" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape8" class="inputs" id="ape8" value="<?php echo $rowp['pcri8'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out9" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape9" class="inputs" id="ape9" value="<?php echo $rowp['pcri9'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out10" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape10" class="inputs" id="ape10" value="<?php echo $rowp['pcri10'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php
											}elseif ($rowcr['cri9']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" class="inputs" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out7" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape7" class="inputs" id="ape7" value="<?php echo $rowp['pcri7'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out8" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape8" class="inputs" id="ape8" value="<?php echo $rowp['pcri8'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out9" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape9" class="inputs" id="ape9" value="<?php echo $rowp['pcri9'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php	
											} elseif ($rowcr['cri8']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" class="inputs" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out7" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape7" class="inputs" id="ape7" value="<?php echo $rowp['pcri7'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out8" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape8" class="inputs" id="ape8" value="<?php echo $rowp['pcri8'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php	
											} elseif ($rowcr['cri7']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" class="inputs" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out7" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape7" class="inputs" id="ape7" value="<?php echo $rowp['pcri7'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php		
											} elseif ($rowcr['cri6']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" class="inputs" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php							
											} elseif ($rowcr['cri5']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php						
											} elseif ($rowcr['cri4']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php					
											} elseif ($rowcr['cri3']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php
											} elseif ($rowcr['cri2']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php	
											} elseif ($rowcr['cri1']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php	
											}else{?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php	
											} 
										}
										 
										  ?>
							</div>
							
						</div>
						
						<div class="modal-footer">
							<button type="submit" name="insert" id="insert" position="center" class="btn btn-success">Actualizar</button>
							<button type="button" data-dismiss="modal" class="btn btn-default">Cerrar</button>
						</div>

				</form>
			</div>	
			

			<div id="valor" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="420">
				<form method="POST" id="valorform">
						<div class="modal-header">
							<button type="button" class="close" data-dismiss="modal" aria-hidden="true"></button>
							<h4 class="modal-title">Valorar Criterios</h4>
						</div>

						<div class="modal-body" id ="valorado">
								
						</div>

						<div class="modal-footer">
							<button type="submit" name="valorar" id="valorar" position="center" class="btn btn-success" >Valorar</button>
							<button type="button" data-dismiss="modal" class="btn btn-default">Cerrar</button>
						</div>

						<input type="text" name="idp" id="idp" style="width: 50px; height: 30px;display:none"/>
						<input type="text" name="tmp" id="tmp" style="width: 50px; height: 30px;display:none"/>
						<input type="text" name="tprov" id="tprov" style="width: 50px; height: 30px;display:none"/>

				</form>
			</div>


			<form method="POST" id="formtab3" action="insert3.php">	
					<h4 class="block col-md-6"><b>Evaluación y Seleccion del Proveedor</b></h4>
					<div class="col-md-12">
						<div class="form-group">	
							<label class="control-label col-md-1">Proveedor 1<span class="required">
							* </span>
							</label>
							
							<span class="btn blue fileinput-button" style="left: 40px;">
								<i class="fa fa-file" id="control" name="control"></i>
								<input type="file" id="cot" name="cot">
							</span>
							<b><span class="col-md-1" type="number" name="total"  id="total" style="left:700px; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>
							<a class="btn yellow" style="left: 75px;" data-toggle="modal" href="#valor" id="evaluador" name="evaluador"> Evaluar </a>
							<div class="col-md-3 proveedor1" style="left: -70px;">
								<select class="form-control input-xlarge select2me proveedor1" data-placeholder="Select..." name="p1" id="p1">
									<option value=""></option>
								</select>
								
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1">Proveedor 2<span class="required">
							* </span>
							</label>

							<span class="btn blue fileinput-button" style="left: 40px;">
								<i class="fa fa-file" id="control1" name="control1"></i>
								<input type="file" id="cot1" name="cot1">
							</span>

							<b><span class="col-md-1" type="number" name="total1"  id="total1" style="left:700px; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: 75px;" data-toggle="modal" href="#valor" id="evaluador1" name="evaluador1"> Evaluar </a>
							<div class="col-md-3 proveedor2" style="left: -70px;">
								<select class="form-control input-xlarge select2me proveedor2" data-placeholder="Select..." name="p2" id="p2">
								
								</select>
								
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1">Proveedor 3<span class="required">
							* </span>
							</label>

							<span class="btn blue fileinput-button" style="left: 40px;">
								<i class="fa fa-file" id="control2" name="control2"></i>
								<input type="file" id="cot2" name="cot2">
							</span>
							<b><span class="col-md-1" type="number" name="total2"  id="total2" style="left:700px; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: 75px;" data-toggle="modal" href="#valor" id="evaluador2" name="evaluador2"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -70px;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p3" id="p3">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1">Proveedor 4<span class="required">
							* </span>
							</label>

							<span class="btn blue fileinput-button" style="left: 40px;">
								<i class="fa fa-file" id="control3" name="control3"></i>
								<input type="file" id="cot3" name="cot3">
							</span>
							<b><span class="col-md-1" type="number" name="total3"  id="total3" style="left:700px; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: 75px;" data-toggle="modal" href="#valor" id="evaluador3" name="evaluador3"> Evaluar </a>
							<div class="col-md-3 proveedor4" style="left: -70px;">
								<select class="form-control input-xlarge select2me proveedor4" data-placeholder="Select..." name="p4" id="p4">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1">Proveedor 5<span class="required">
							* </span>
							</label>
							
							<span class="btn blue fileinput-button" style="left: 40px;">
								<i class="fa fa-file" id="control4" name="control4"></i>
								<input type="file" id="cot4" name="cot4">
							</span>
							<b><span class="col-md-1" type="number" name="total4"  id="total4" style="left:700px; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

							<a class="btn yellow" style="left: 75px;" data-toggle="modal" href="#valor" id="evaluador4" name="evaluador4"> Evaluar </a>
							<div class="col-md-3 proveedor5" style="left: -70px;">
								<select class="form-control input-xlarge select2me proveedor5" data-placeholder="Select..." name="p5" id="p5">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-2">Proveedor Sugerido<span class="required">
							* </span>
							</label>
							<div class="col-md-1 proveedore">
								<input type="text" style="text-align: center" class="form-control input-xlarge select2me proveedor" name="ps" id="ps" value="" readonly/>
							</div>

							<div class="col-md-1" style="left:320px;padding-top:5px;">
								<input type="checkbox" style="text-align: center; " onclick="captar();" class="md-check" name="psug"      id="psug"/><label>&nbsp;Otro</label>
							</div>

							<div class="col-md-1 proveedor" style="left:320px;">	
								<select type = "text" style="text-align: center" class="form-control input-xlarge select2me proveedor" data-placeholder="Select..." name="pe" id="pe" disabled>
									<option value=""></option>
								</select >	
							</div>
						</div>
						<input type="text" name="pelegido" id="pelegido" style="display:none;">
						<input type="text" name="cote" id="cote" style="display:none;">
						<input type="text" name="cote1" id="cote1" style="display:none;">
						<input type="text" name="cote2" id="cote2" style="display:none;">
						<input type="text" name="cote3" id="cote3" style="display:none;">
						<input type="text" name="cote4" id="cote4" style="display:none;">
					</div>

					<div class="col-md-12">
						<div class="form-group" style="text-align:center;">
							<div class="col-md-3" style="left:80px;top:30px;">
								<label>Comentario <span class="required" style="color:red">
							* </span></label>
							</div>
							<textarea placeholder="Comentario..." id="comentotro" name="comentotro" class="form-control" style="margin: 0px;width: 706px;height: 86px;" required></textarea>
						</div>
					</div>
					
					<a class="btn default col-md-offset-1" data-toggle="modal" href="#valoraciones">
					Ver Criterios</a>
					
				<div class="row">
					<div class="col-md-offset-5 col-md-8">
						<input type="submit" name="insert" position="center" class="btn btn-success" value="Registrar"> 	
					</div>
				</div>
			</form>

			<div class="form-actions">
				<div class="row-a">
					<div class="col-md-1" style="display:block;" id="atras2">
						<a href="javascript:;" class="btn blue button-previous" id="atras">
						<i class="m-icon-swapleft m-icon-white"></i></a>
					</div>
					<div class="col-md-1" style="display:none" id="siguiente2">				
						<a href="javascript:;" class="btn green button-next" id="siguiente">
						<i class="m-icon-swapright m-icon-white"></i>
						</a>
					</div>
					<div class="col-md-offset-1 col-md-9" style="display:none" id="fin2">
						<a href="javascript:;" class="btn yellow button-submit" id="fin">
						Finalizar <i class="m-icon-swapright m-icon-white"></i>  
						</a>
						
					</div>
				</div>
			</div>

			<?php
			}else{
			?>	
			<div id="valoraciones" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="40%" style="width:40%;">
				<form method="POST" id="critform">
						<div class="modal-header">
							<button type="button" class="close" data-dismiss="modal" aria-hidden="true"></button>
							<h4 class="modal-title">Matriz de Criterios para la Evaluación de Proveedores</h4>
						</div>
						<div class="modal-body">
						<?php
							while($crq = mysqli_fetch_array($controlado,MYSQLI_ASSOC))
								{
						?> 
							<fieldset>
								<label><b>Criterios Globales de Elección</b></label>
								<br>
								<input type="text" name="anuncio" id="anuncio" value="La suma de Porcentajes es 100" class="form-control input-slarge" style="border:none;text-align:center;font-size:12px;color:green;font-weight: bold;">
								<div class="col-md-12">
								<div class="col-md-6">
								<label style="margin-left:20%;">Evaluación Económica (%):</label><input type="number" min="40" max="50" value="<?php echo $crq['ee'];?>" name="peconomico" id="peconomico" class="form-control input-xsmall" onchange="comprobar()" style="margin-left: 35%;text-align:center;" readonly/>	
								</div>
								<div class="col-md-6">
								<label style="margin-left:20%;">Evaluación Técnica (%):</label><input type="number" name="ptecnico"  value="<?php echo $crq['et'];?>" id="ptecnico" class="form-control input-xsmall" onchange="comprobar2()" style="margin-left: 30%;text-align:center;" readonly>
								<br>
								</div>
								</div>
								<br>

							</fieldset>
							<fieldset>
								<label><b>Evaluación Económica (S/.)</b> </label><label style="font-size:12px;"> - A continuación se muestran los montos cotizados por cada proveedor</label>
								<br>
								<div class="col-md-12">
								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Proveedor 1:</label></div>
									<div class="col-md-4"><input type="number"  name="ppro1" id="ppro1" class="form-control input-small" style="text-align:center;" value="<?php echo $crq['pp1'];?>" readonly />	</div>
								</div>
								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Proveedor 2:</label></div>
									<div class="col-md-4"><input type="number"   name="ppro2" id="ppro2" class="form-control input-small" style="text-align:center;" value="<?php echo $crq['pp2'];?>" readonly />		</div>
								</div>
								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Proveedor 3:</label></div>
									<div class="col-md-4"><input type="number"  name="ppro3" id="ppro3" class="form-control input-small"  style="text-align:center;"  value="<?php echo $crq['pp3'];?>" readonly/>	</div>		
								</div>

								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Proveedor 4:</label></div>
									<div class="col-md-4"><input type="number"   name="ppro4" id="ppro4" class="form-control input-small"  style="text-align:center;" value="<?php echo $crq['pp4'];?>" readonly/>	</div>		
								</div>
								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Proveedor 5:</label></div>
									<div class="col-md-4"><input type="number"  name="ppro5" id="ppro5" class="form-control input-small"  style="text-align:center;" value="<?php echo $crq['pp5'];?>" readonly />	</div>
								</div>
								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Valor Minimo:</label></div>
									<div class="col-md-4"><input type="number"  name="pminimo" id="pminimo" class="form-control input-small" style="text-align:center;" readonly value="<?php echo $crq['vm'];?>" readonly/>	</div>
								</div>
								<br>
								</div>
								<br>

							</fieldset>
							<?php
							}
							?>
							<fieldset>
								<br>
								      <label><b>Evaluación Técnica</b> </label>
								      <br>
								      <!-- <input type="button" id="btnAdd" value="+" class="btn green" />
								      <input type="button" id="btnDel" value="-" class="btn red"/> -->
								     <label style="color: red; padding-left: 50%;"><b>TOTAL: <input type="number" name="pesos" id="pesos" style="width: 40px;border:none;background-color:white;" value="100" disabled></b><b>%</b></label>
							</fieldset>
							<div class="col-md-5">
									<p>
									<label>Criterios</label>
									<hr>
									</p>
								      <?php
										while($rowc = mysqli_fetch_array($resultadoc,MYSQLI_ASSOC))
											{
											if($rowc['cri10']!=""){?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px; border:none;" readonly"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input7" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name7" id="name7" value="<?php echo $rowc['cri7'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input8" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name8" id="name8" value="<?php echo $rowc['cri8'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input9" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name9" id="name9" value="<?php echo $rowc['cri9'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input10" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name10" id="name10" value="<?php echo $rowc['cri10'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<?php
											}elseif ($rowc['cri9']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input7" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name7" id="name7" value="<?php echo $rowc['cri7'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input8" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name8" id="name8" value="<?php echo $rowc['cri8'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input9" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name9" id="name9" value="<?php echo $rowc['cri9'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<?php	
											} elseif ($rowc['cri8']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input7" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name7" id="name7" value="<?php echo $rowc['cri7'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input8" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name8" id="name8" value="<?php echo $rowc['cri8'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<?php	
											} elseif ($rowc['cri7']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input7" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name7" id="name7" value="<?php echo $rowc['cri7'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<?php		
											} elseif ($rowc['cri6']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<?php							
											} elseif ($rowc['cri5']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<?php						
											} elseif ($rowc['cri4']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<?php					
											} elseif ($rowc['cri3']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<?php
											} elseif ($rowc['cri2']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<?php	
											} elseif ($rowc['cri1']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<?php	
											}else{?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" style="width: 200px; height: 30px; border:none;" readonly/>
											</fieldset>
											<?php	
											} 
										}?>
							</div>

							<div class="col-md-7" style="left: 40px;">
								<p>
									<label>Peso (%) </label>
									<hr>
								</p>
								<?php
										while($rowcr = mysqli_fetch_array($resultadocr,MYSQLI_ASSOC) and $rowp = mysqli_fetch_array($resultadop,MYSQLI_ASSOC))
											{
											if($rowcr['cri10']!=""){?>
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" id="nape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out7" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape7" id="ape7" value="<?php echo $rowp['pcri7'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out8" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape8" id="ape8" value="<?php echo $rowp['pcri8'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out9" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape9" id="ape9" value="<?php echo $rowp['pcri9'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out10" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape10" id="ape10" value="<?php echo $rowp['pcri10'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<?php
											}elseif ($rowcr['cri9']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" id="nape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out7" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape7" id="ape7" value="<?php echo $rowp['pcri7'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out8" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape8" id="ape8" value="<?php echo $rowp['pcri8'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out9" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape9" id="ape9" value="<?php echo $rowp['pcri9'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<?php	
											} elseif ($rowcr['cri8']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" id="nape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out7" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape7" id="ape7" value="<?php echo $rowp['pcri7'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out8" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape8" id="ape8" value="<?php echo $rowp['pcri8'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<?php	
											} elseif ($rowcr['cri7']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" id="nape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out7" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape7" id="ape7" value="<?php echo $rowp['pcri7'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<?php		
											} elseif ($rowcr['cri6']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" id="nape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<?php							
											} elseif ($rowcr['cri5']!="") {?>
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" id="nape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<?php						
											} elseif ($rowcr['cri4']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" id="nape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<?php					
											} elseif ($rowcr['cri3']!="") {?>
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" id="nape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<?php
											} elseif ($rowcr['cri2']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" id="nape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<?php	
											} elseif ($rowcr['cri1']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<?php	
											}else{?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" id="ape1" style="width: 50px; height: 30px; border:none;text-align: center;" readonly/>
											</fieldset>
											<?php	
											} 
										}?>
							</div>
						</div>
						<div class="modal-footer">
							<button type="button" data-dismiss="modal" class="btn btn-default">Cerrar</button>
						</div>
				</form>
			</div>	
			<!-- <div id="valor1" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="1200" style="margin-top: 5%;margin-left:-35%">  -->
			<div id="valor1" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="420">
				<form method="POST" id="valorform1">
						<div class="modal-header">
							<button type="button" class="close" data-dismiss="modal" aria-hidden="true"></button>
							<h4 class="modal-title">Criterios Valorados</h4>
						</div>

						<div class="modal-body" id ="valorado1">
								
						</div>

						<div class="modal-footer">
							<button type="button" data-dismiss="modal" class="btn btn-default">Cerrar</button>
						</div>

						<input type="text" name="idp" id="idp" style="width: 50px; height: 30px;display:none"/>
						<input type="text" name="tmp" id="tmp" style="width: 50px; height: 30px;display:none"/>
						<input type="text" name="tprov" id="tprov" style="width: 50px; height: 30px;display:none"/>

				</form>
			</div>

			<div id="resumentablero" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="1000" style="margin-top:2%; margin-left:-38%; height:auto;" >  
			<!-- <div id="valor1" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="420"> -->
				<form method="POST" id="resumentableroform" style="overflow-y: hidden;">
						<div class="modal-header">
							<button type="button" class="close" data-dismiss="modal" aria-hidden="true"></button>
							<h4 class="modal-title">Resultado de Evaluación</h4>
						</div>

						<div class="modal-body" id ="resumentab" name ="resumentab" style="overflow-y: scroll;" >
								
						</div>

						<div class="modal-footer">
							<button type="button" data-dismiss="modal" class="btn btn-default">Cerrar</button>
						</div>

						<input type="text" name="idp" id="idp" style="width: 50px; height: 30px;display:none"/>
						<input type="text" name="tmp" id="tmp" style="width: 50px; height: 30px;display:none"/>
						<input type="text" name="tprov" id="tprov" style="width: 50px; height: 30px;display:none"/>

				</form>
			</div>
				<div class="col-md-12">
						<h4 class="block col-md-6"><b>Evaluación y Seleccion del Proveedor</b></h4>

				</div>
				<div class="col-md-12">
						<h4 class="block col-md-6"><b>Proveedor</b></h4>
						<h4 class="block col-md-1" style="left:-18%;"><b>Descargar</b></h4>
						<a class="btn default" data-toggle="modal" href="#valoraciones" style="left:-16%">
					Ver Criterios</a>
				</div>
				<?php 
				while($rowsel = mysqli_fetch_array($seleccionado,MYSQLI_ASSOC) and $rprp = mysqli_fetch_array($prrp,MYSQLI_ASSOC))
				{
					if ($rprp['cotizaciones'] == 3) {
						$_SESSION['cot1'] = '<span class="required">
							* </span>';
						$_SESSION['cot2'] = '<span class="required">
							* </span>';
						$_SESSION['cot3'] = '<span class="required">
							* </span>';
					}elseif ($rprp['cotizaciones'] == 2) {
						$_SESSION['cot1'] = '<span class="required">
							* </span>';
						$_SESSION['cot2'] = '<span class="required">
							* </span>';
						$_SESSION['cot3'] = '';	
					}elseif ($rprp['cotizaciones'] == 1) {
						$_SESSION['cot1'] = '<span class="required">
							* </span>';
							$_SESSION['cot2'] = '';
						$_SESSION['cot3'] = '';
					}
				?>
					<div class="col-md-12">
						<div class="form-group">	
							<label class="control-label col-md-1" style="left:3%;">1 <?php echo $_SESSION['cot1'];?>
							</label>
							<?php if ($row['ruta1'] == "") {
								?>
								<a style="left: -4%;" class="btn gray fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Cotización</a>

								<b><span class="col-md-1" type="number" name="total"  id="total" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

								 <a class="btn gray" style="left: -3%;" data-toggle="modal"> Sin Evaluación </a>

							<?php
							}else{

							?>
								<a href="descargac.php?archivo=<?php echo $row['ruta1'];?>" style="left: -4%;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Cotización</a>

								 <b><span class="col-md-1" type="number" name="total"  id="total" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

								 <a class="btn green" style="left: -3%;" data-toggle="modal" href="#valor1" id="evaluacion" name="evaluacion"> Ver Evaluación </a>
							<?php	
							}
							?>
							 
							<div class="col-md-3 proveedor1" style="left: -5%;">
								<select class="form-control input-slarge select2me proveedor1" data-placeholder="Select..." name="p1" id="p1" disabled>
									<option value=""></option>
								</select>
								
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1" style="left:3%;">2 <?php echo $_SESSION['cot2'];?>
							</label>

							<?php if ($row['ruta2'] == "") {
								?>
								<a  style="left: -4%;" class="btn gray fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Cotización</a>

								<b><span class="col-md-1" type="number" name="total1"  id="total1" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

								 <a class="btn gray" style="left: -3%;" data-toggle="modal"> Sin Evaluación </a>

							<?php
							}else{

							?>
								<a href="descargac.php?archivo=<?php echo $row['ruta2'];?>" style="left: -4%;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Cotización</a>

								<b><span class="col-md-1" type="number" name="total1"  id="total1" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

								<a class="btn green" style="left: -3%;" data-toggle="modal" href="#valor1" id="evaluacion1" name="evaluacion1"> Ver Evaluación </a>
							<?php	
							}
							?>

							
							<div class="col-md-3 proveedor2" style="left: -5%;">
								<select class="form-control input-slarge select2me proveedor2" data-placeholder="Select..." name="p2" id="p2" disabled>
								
								</select>
								
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1" style="left:3%;">3 <?php echo $_SESSION['cot3'];?>
							</label>


							<?php if ($row['ruta3'] == "") {
								?>
								<a  style="left: -4%;" class="btn gray fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Cotización</a>

								<b><span class="col-md-1" type="number" name="total2"  id="total2" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

								 <a class="btn gray" style="left: -3%;" data-toggle="modal"> Sin Evaluación </a>

							<?php
							}else{

							?>
								<a href="descargac.php?archivo=<?php echo $row['ruta3'];?>" style="left: -4%;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Cotización</a>

								<b><span class="col-md-1" type="number" name="total2"  id="total2" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

								<a class="btn green" style="left: -3%" data-toggle="modal" href="#valor1" id="evaluacion2" name="evaluacion2"> Ver Evaluación </a>

							<?php	
							}
							?>

							<a class="btn" style="left: 20%;color: #FFFFFF; background-color: rgba(255, 79, 0, 1);" id="resumido" name="resumido"> Resultado de Evaluación </a>
							
							<div class="col-md-3 proveedor3" style="left: -5%;">
								<select class="form-control input-slarge select2me proveedor3" data-placeholder="Select..." name="p3" id="p3" disabled>
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1" style="left:3%;">4</label>

							<?php if ($row['ruta4'] == "") {
								?>
								<a  style="left: -4%;" class="btn gray fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Cotización</a>

								<b><span class="col-md-1" type="number" name="total3"  id="total3" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

								 <a class="btn gray" style="left: -3%;" data-toggle="modal"> Sin Evaluación </a>

							<?php
							}else{

							?>
								<a href="descargac.php?archivo=<?php echo $row['ruta4'];?>" style="left: -4%;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Cotización</a>
							
								<b><span class="col-md-1" type="number" name="total3"  id="total3" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

								<a class="btn green" style="left: -3%;" data-toggle="modal" href="#valor1" id="evaluacion3" name="evaluacion3"> Ver Evaluación </a>
							<?php	
							}
							?>

							
							<div class="col-md-3 proveedor4" style="left: -5%;">
								<select class="form-control input-slarge select2me proveedor4" data-placeholder="Select..." name="p3" id="p3" disabled>
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1" style="left:3%;">5</label>

							<?php if ($row['ruta5'] == "") {
								?>
								<a style="left: -4%;" class="btn gray fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Cotización</a>

								<b><span class="col-md-1" type="number" name="total4"  id="total4" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

								 <a class="btn gray" style="left: -3%;" data-toggle="modal" > Sin Evaluación </a>

							<?php
							}else{

							?>
								<a href="descargac.php?archivo=<?php echo $row['ruta5'];?>" style="left: -4%;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Cotización</a>

								<b><span class="col-md-1" type="number" name="total4"  id="total4" style="left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;" readonly> </span></b>

								<a class="btn green" style="left: -3%;" data-toggle="modal" href="#valor1" id="evaluacion4" name="evaluacion4"> Ver Evaluación </a>
							<?php	
							}
							?>
							
							
							<div class="col-md-3 proveedor5" style="left: -5%;">
								<select class="form-control input-slarge select2me proveedor45" data-placeholder="Select..." name="p3" id="p3" disabled>
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>
					
					
					<div id="responsive" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="380">
						<div class="modal-header">
							<button type="button" class="close" data-dismiss="modal" aria-hidden="true"></button>
							<h4 class="modal-title">Nuevo Proveedor</h4>
						</div>
						<div class="modal-body">
							<div class="row">
								<div class="col-md-6">
									<h4></h4>
									<p>
										<label>Nombre del Proveedor</label>
										<input class="form-control" type="text">
									</p>
									<p>
										<label>RUC</label>	
										<input class="form-control" type="text">
									</p>
									<p>
										<label>Dirección</label>
										<input class="form-control" type="text">
									</p>
									<p>
										<label>Persona de Contacto</label>
										<input class="form-control" type="text">
									</p>
									<p>
										<label>Teléfono</label>
										<input class="form-control" type="text">
									</p>
								</div>
								

						</div>
					</div>
					<div class="modal-footer">
							<button type="button" data-dismiss="modal" class="btn btn-default">Close</button>
							<button type="button" class="btn blue">Save changes</button>
					</div>
				</div>
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-2">Ganador del concurso
							</label>
							<div class="col-md-3"  style="left:-5%;">
								<input type="text" class="form-control input-slarge" style="text-align:center;" name="prove" id="prove" value="<?php echo $rowsel['prove'];?>" readonly/>
							</div>
						</div>
						<input type="text" name="pelegido" id="pelegido" style="display:none;">
						<input type="text" name="cote" id="cote" style="display:none;">
						<input type="text" name="cote1" id="cote1" style="display:none;">
						<input type="text" name="cote2" id="cote2" style="display:none;">
						<input type="text" name="cote3" id="cote3" style="display:none;">
						<input type="text" name="cote4" id="cote4" style="display:none;">
					</div>

					<div class="col-md-12">
						<div class="form-group" style="text-align:center;">
							<div class="col-md-3" style="left:80px;top:30px;">
								<label>Sustento del Cambio <span class="required" style="color:red">
							* </span></label>
							</div>
							<textarea  id="comentotro" name="comentotro" class="form-control" style="margin: 0px;width: 706px;height: 86px;" disabled><?php echo $rowsel['comentario'];?></textarea>
						</div>
					</div>
				<?php
				
				}
				
				?>

				<?php

				if($rows['acepsel'] =='si'){

					?>
				<div class="form-actions">
					<div class="row-a">
						<div class="col-md-1" style="display:block;" id="atras2">
							<a href="javascript:;" class="btn blue button-previous" id="atras">
							<i class="m-icon-swapleft m-icon-white"></i></a>
						</div>
						<div class="col-md-1" style="display:block;float: right;" id="siguiente2">				
							<a href="javascript:;" class="btn green button-next" id="siguiente">
							<i class="m-icon-swapright m-icon-white"></i>
							</a>
						</div>
						<div class="col-md-offset-1 col-md-9" style="display:none" id="fin2">
							<a href="javascript:;" class="btn yellow button-submit" id="fin">
							Finalizar <i class="m-icon-swapright m-icon-white"></i>  
							</a>
							
						</div>
					</div>
				</div>
				<?php
					} else{
						?>
				<div class="form-actions">
					<div class="row-a">
						<div class="col-md-1" style="display:block;" id="atras2">
							<a href="javascript:;" class="btn blue button-previous" id="atras">
							<i class="m-icon-swapleft m-icon-white"></i></a>
						</div>
						<div class="col-md-1" style="display:none" id="siguiente2">				
							<a href="javascript:;" class="btn green button-next" id="siguiente">
							<i class="m-icon-swapright m-icon-white"></i>
							</a>
						</div>
						<div class="col-md-offset-1 col-md-9" style="display:none" id="fin2">
							<a href="javascript:;" class="btn yellow button-submit" id="fin">
							Finalizar <i class="m-icon-swapright m-icon-white"></i>  
							</a>
							
						</div>
					</div>
				</div>
						<?php
					}
				?>
			<?php
			}
		}
	}
	if(mysqli_num_rows($resultado4)< 1){
		?>
				<div id="criterios" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="40%">
					<form method="POST" id="critform1">
						<div class="modal-header">
							<button type="button" class="close" data-dismiss="modal" aria-hidden="true"></button>
							<h4 class="modal-title">Matriz de Criterios para la Evaluación de Proveedores</h4>
						</div>
						<div class="modal-body">
						<?php
							while($crq = mysqli_fetch_array($controlte,MYSQLI_ASSOC))
								{
						?> 
							<fieldset>
								<label><b>Criterios Globales de Elección</b></label>
								<br>
								<input type="text" name="anuncio" id="anuncio" value="La suma de Porcentajes debe ser 100" class="form-control input-slarge" style="border:none;text-align:center;font-size:12px;color:orange;font-weight: bold;">
								<div class="col-md-12">
								<div class="col-md-6">
								<label style="margin-left:20%;">Evaluación Económica (%):</label><input type="number" min="40" max="50" value="<?php echo $crq['ee'];?>" name="peconomico" id="peconomico" class="form-control input-xsmall" onchange="comprobar()" style="margin-left: 35%;text-align:center;" />	
								</div>
								<div class="col-md-6">
								<label style="margin-left:20%;">Evaluación Técnica (%):</label><input type="number" name="ptecnico"  value="<?php echo $crq['et'];?>" id="ptecnico" class="form-control input-xsmall" onchange="comprobar2()" style="margin-left: 30%;text-align:center;" >
								<br>
								</div>
								</div>
								<br>

							</fieldset>
							<fieldset>
								<label><b>Evaluación Económica (S/.)</b> </label><label style="font-size:12px;"> - A continuación se muestran los montos cotizados por cada proveedor</label>
								<br>
								<div class="col-md-12">
								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Proveedor 1:</label></div>
									<div class="col-md-4"><input type="number"  name="ppro1" id="ppro1" class="form-control input-small" value="0" style="text-align:center;" value="<?php echo $crq['pp1'];?>" />	</div>
								</div>
								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Proveedor 2:</label></div>
									<div class="col-md-4"><input type="number"   name="ppro2" id="ppro2" class="form-control input-small" value="0" style="text-align:center;" value="<?php echo $crq['pp2'];?>" />		</div>
								</div>
								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Proveedor 3:</label></div>
									<div class="col-md-4"><input type="number"  name="ppro3" id="ppro3" class="form-control input-small" value="0" style="text-align:center;"  value="<?php echo $crq['pp3'];?>" />	</div>		
								</div>

								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Proveedor 4:</label></div>
									<div class="col-md-4"><input type="number"   name="ppro4" id="ppro4" class="form-control input-small" value="0" style="text-align:center;" value="<?php echo $crq['pp4'];?>" />	</div>		
								</div>
								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Proveedor 5:</label></div>
									<div class="col-md-4"><input type="number"  name="ppro5" id="ppro5" class="form-control input-small" value="0" style="text-align:center;" value="<?php echo $crq['pp5'];?>" />	</div>
								</div>
								<div class="col-md-6" style="left:-5%;">
									<div class="col-md-6"><label style="padding-top:5%;">Valor Minimo:</label></div>
									<div class="col-md-4"><input type="number"  name="pminimo" id="pminimo" class="form-control input-small" value="0" style="text-align:center;" readonly value="<?php echo $crq['vm'];?>"/>	</div>
								</div>
								<br>
								</div>
								<br>

							</fieldset>
							<?php
							}
							?>
							<fieldset>
								<br>
								      <label><b>Evaluación Técnica</b> </label>
								      <br>
								      <!-- <input type="button" id="btnAdd" value="+" class="btn green" />
								      <input type="button" id="btnDel" value="-" class="btn red"/> -->
								     <label style="color: red; padding-left: 50%;"><b>TOTAL: <input type="number" name="pesos" id="pesos" style="width: 40px;border:none;background-color:white;" value="" disabled></b><b>%</b></label>
							</fieldset>	
							<div class="col-md-7">
									<p>
									<label>Criterios</label>
									</p>
								      <?php
										while($rowc = mysqli_fetch_array($resultadoc,MYSQLI_ASSOC))
											{
											if($rowc['cri10']!=""){?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input7" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name7" id="name7" value="<?php echo $rowc['cri7'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input8" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name8" id="name8" value="<?php echo $rowc['cri8'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input9" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name9" id="name9" value="<?php echo $rowc['cri9'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input10" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name10" id="name10" value="<?php echo $rowc['cri10'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php
											}elseif ($rowc['cri9']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input7" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name7" id="name7" value="<?php echo $rowc['cri7'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input8" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name8" id="name8" value="<?php echo $rowc['cri8'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input9" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name9" id="name9" value="<?php echo $rowc['cri9'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php	
											} elseif ($rowc['cri8']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input7" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name7" id="name7" value="<?php echo $rowc['cri7'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input8" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name8" id="name8" value="<?php echo $rowc['cri8'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php	
											} elseif ($rowc['cri7']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input7" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name7" id="name7" value="<?php echo $rowc['cri7'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php		
											} elseif ($rowc['cri6']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input6" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name6" id="name6" value="<?php echo $rowc['cri6'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php							
											} elseif ($rowc['cri5']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input5" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name5" id="name5" value="<?php echo $rowc['cri5'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php						
											} elseif ($rowc['cri4']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input4" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name4" id="name4" value="<?php echo $rowc['cri4'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php					
											} elseif ($rowc['cri3']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input3" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name3" id="name3" value="<?php echo $rowc['cri3'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php
											} elseif ($rowc['cri2']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<fieldset id="input2" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name2" id="name2" value="<?php echo $rowc['cri2'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php	
											} elseif ($rowc['cri1']!="") {?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" value="<?php echo $rowc['cri1'];?>" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php	
											}else{?> 
											<fieldset id="input1" class="clonedInput" style="margin-bottom: 10px;">
											<input type="text" name="name1" id="name1" style="width: 200px; height: 30px"/>
											</fieldset>
											<?php	
											} 
										}?>
							</div>

							<div class="col-md-5" style="left: 40px;">
								<p>
									<label>Peso (%) </label>
								</p>
								<?php
										while($rowcr = mysqli_fetch_array($resultadocr,MYSQLI_ASSOC) and $rowp = mysqli_fetch_array($resultadop,MYSQLI_ASSOC))
											{
											if($rowcr['cri10']!=""){?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" class="inputs" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out7" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape7" class="inputs" id="ape7" value="<?php echo $rowp['pcri7'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out8" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape8" class="inputs" id="ape8" value="<?php echo $rowp['pcri8'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out9" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape9" class="inputs" id="ape9" value="<?php echo $rowp['pcri9'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out10" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape10" class="inputs" id="ape10" value="<?php echo $rowp['pcri10'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php
											}elseif ($rowcr['cri9']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" class="inputs" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out7" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape7" class="inputs" id="ape7" value="<?php echo $rowp['pcri7'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out8" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape8" class="inputs" id="ape8" value="<?php echo $rowp['pcri8'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out9" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape9" class="inputs" id="ape9" value="<?php echo $rowp['pcri9'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php	
											} elseif ($rowcr['cri8']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" class="inputs" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out7" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape7" class="inputs" id="ape7" value="<?php echo $rowp['pcri7'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out8" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape8" class="inputs" id="ape8" value="<?php echo $rowp['pcri8'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php	
											} elseif ($rowcr['cri7']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" class="inputs" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out7" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape7" class="inputs" id="ape7" value="<?php echo $rowp['pcri7'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php		
											} elseif ($rowcr['cri6']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out6" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape6" class="inputs" id="ape6" value="<?php echo $rowp['pcri6'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php							
											} elseif ($rowcr['cri5']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out5" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape5" class="inputs" id="ape5" value="<?php echo $rowp['pcri5'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php						
											} elseif ($rowcr['cri4']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out4" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape4" class="inputs" id="ape4" value="<?php echo $rowp['pcri4'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php					
											} elseif ($rowcr['cri3']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out3" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape3" class="inputs" id="ape3" value="<?php echo $rowp['pcri3'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php
											} elseif ($rowcr['cri2']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<fieldset id="out2" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape2" class="inputs" id="ape2" value="<?php echo $rowp['pcri2'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php	
											} elseif ($rowcr['cri1']!="") {?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" value="<?php echo $rowp['pcri1'];?>" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php	
											}else{?> 
											<fieldset id="out1" class="clonedOut" style="margin-bottom: 10px;">
											<input type="number" name="ape1" class="inputs" id="ape1" style="width: 50px; height: 30px;text-align: center;"/>
											</fieldset>
											<?php	
											} 
										}
										 
										  ?>
							</div>
						</div>

						<div class="modal-footer">
							<button type="submit" position="center" class="btn btn-success" id="registrar" name="registrar">Registrar</button>
							<button type="button" data-dismiss="modal" class="btn btn-default">Cerrar</button>
						</div>

				</form>
			</div>

			<div id="valor" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="420">
				<form method="POST" id="valorform">
						<div class="modal-header">
							<button type="button" class="close" data-dismiss="modal" aria-hidden="true"></button>
							<h4 class="modal-title">Valorar Criterios</h4>
						</div>

						<div class="modal-body" id ="valorado">
								
						</div>

						<div class="modal-footer">
							<button type="submit" name="valorar" id="valorar" position="center" class="btn btn-success">Valorar</button>
							<button type="button" data-dismiss="modal" class="btn btn-default">Cerrar</button>
						</div>

						<input type="text" name="idp" id="idp" style="width: 50px; height: 30px;display:none"/>
						<input type="text" name="tmp" id="tmp" style="width: 50px; height: 30px;display:none"/>
						<input type="text" name="tprov" id="tprov" style="width: 50px; height: 30px;display:none"/>

				</form>
			</div>
				<form method="POST" id="formtab3" action="insert3.php">	
					<h4 class="block col-md-6"><b>Evaluación y Seleccion del Proveedor</b></h4>
					<?php

					while($mando = mysqli_fetch_array($tblmando,MYSQLI_ASSOC))
					{
					if($mando['cotizaciones'] == 3){

					?>
					<div class="col-md-12">
						<div class="form-group">	
							<label class="control-label col-md-1">Proveedor 1<span class="required">
							* </span>
							</label>
							
							<span class="btn blue fileinput-button" style="left: 90px;">
								<i class="fa fa-file" id="control" name="control"></i>
								<input type="file" id="cot" name="cot">
							</span>

							<a class="btn yellow" style="left: 120px;" data-toggle="modal" href="#valor" id="evaluador" name="evaluador"> Evaluar </a>
							<div class="col-md-3 proveedor1" style="left: -20px;">
								<select class="form-control input-xlarge select2me proveedor1" data-placeholder="Select..." name="p1" id="p1">
									<option value=""></option>
								</select>
								
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1">Proveedor 2<span class="required">
							* </span>
							</label>

							<span class="btn blue fileinput-button" style="left: 90px;">
								<i class="fa fa-file" id="control1" name="control1"></i>
								<input type="file" id="cot1" name="cot1">
							</span>


							<a class="btn yellow" style="left: 120px;" data-toggle="modal" href="#valor" id="evaluador1" name="evaluador1"> Evaluar </a>
							<div class="col-md-3 proveedor2" style="left: -20px;">
								<select class="form-control input-xlarge select2me proveedor2" data-placeholder="Select..." name="p2" id="p2">
								
								</select>
								
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1">Proveedor 3<span class="required">
							* </span>
							</label>

							<span class="btn blue fileinput-button" style="left: 90px;">
								<i class="fa fa-file" id="control2" name="control2"></i>
								<input type="file" id="cot2" name="cot2">
							</span>
							
							<a class="btn yellow" style="left: 120px;" data-toggle="modal" href="#valor" id="evaluador2" name="evaluador2"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -20px;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p3" id="p3">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1">Proveedor 4
							</label>

							<span class="btn blue fileinput-button" style="left: 90px;">
								<i class="fa fa-file" id="control3" name="control3"></i>
								<input type="file" id="cot3" name="cot3">
							</span>
							
							<a class="btn yellow" style="left: 120px;" data-toggle="modal" href="#valor" id="evaluador3" name="evaluador3"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -20px;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p4" id="p4">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1">Proveedor 5
							</label>
							
							<span class="btn blue fileinput-button" style="left: 90px;">
								<i class="fa fa-file" id="control4" name="control4"></i>
								<input type="file" id="cot4" name="cot4">
							</span>

							<a class="btn yellow" style="left: 120px;" data-toggle="modal" href="#valor" id="evaluador4" name="evaluador4"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -20px;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p5" id="p5">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>
					<?php
				}
				if ($mando['cotizaciones'] == 2)
				{

				?>
				<div class="col-md-12">
						<div class="form-group">	
							<label class="control-label col-md-1">Proveedor 1<span class="required">
							* </span>
							</label>
							
							<span class="btn blue fileinput-button" style="left: 90px;">
								<i class="fa fa-file" id="control" name="control"></i>
								<input type="file" id="cot" name="cot">
							</span>

							<a class="btn yellow" style="left: 120px;" data-toggle="modal" href="#valor" id="evaluador" name="evaluador"> Evaluar </a>
							<div class="col-md-3 proveedor1" style="left: -20px;">
								<select class="form-control input-xlarge select2me proveedor1" data-placeholder="Select..." name="p1" id="p1">
									<option value=""></option>
								</select>
								
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1">Proveedor 2<span class="required">
							* </span>
							</label>

							<span class="btn blue fileinput-button" style="left: 90px;">
								<i class="fa fa-file" id="control1" name="control1"></i>
								<input type="file" id="cot1" name="cot1">
							</span>


							<a class="btn yellow" style="left: 120px;" data-toggle="modal" href="#valor" id="evaluador1" name="evaluador1"> Evaluar </a>
							<div class="col-md-3 proveedor2" style="left: -20px;">
								<select class="form-control input-xlarge select2me proveedor2" data-placeholder="Select..." name="p2" id="p2">
								
								</select>
								
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1">Proveedor 3
							</label>

							<span class="btn blue fileinput-button" style="left: 90px;">
								<i class="fa fa-file" id="control2" name="control2"></i>
								<input type="file" id="cot2" name="cot2">
							</span>
							
							<a class="btn yellow" style="left: 120px;" data-toggle="modal" href="#valor" id="evaluador2" name="evaluador2"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -20px;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p3" id="p3">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1">Proveedor 4
							</label>

							<span class="btn blue fileinput-button" style="left: 90px;">
								<i class="fa fa-file" id="control3" name="control3"></i>
								<input type="file" id="cot3" name="cot3">
							</span>
							
							<a class="btn yellow" style="left: 120px;" data-toggle="modal" href="#valor" id="evaluador3" name="evaluador3"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -20px;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p4" id="p4">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1">Proveedor 5
							</label>
							
							<span class="btn blue fileinput-button" style="left: 90px;">
								<i class="fa fa-file" id="control4" name="control4"></i>
								<input type="file" id="cot4" name="cot4">
							</span>

							<a class="btn yellow" style="left: 120px;" data-toggle="modal" href="#valor" id="evaluador4" name="evaluador4"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -20px;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p5" id="p5">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>
				<?php
				}
				if ($mando['cotizaciones'] == 1)
				{

				?>
				<div class="col-md-12">
						<div class="form-group">	
							<label class="control-label col-md-1">Proveedor 1<span class="required" style="color:red">
							* </span>
							</label>
							
							<span class="btn blue fileinput-button" style="left: 90px;">
								<i class="fa fa-file" id="control" name="control"></i>
								<input type="file" id="cot" name="cot">
							</span>

							<a class="btn yellow" style="left: 120px;" data-toggle="modal" href="#valor" id="evaluador" name="evaluador"> Evaluar </a>
							<div class="col-md-3 proveedor1" style="left: -20px;">
								<select class="form-control input-xlarge select2me proveedor1" data-placeholder="Select..." name="p1" id="p1">
									<option value=""></option>
								</select>
								
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1">Proveedor 2<span class="required" style="color:red">
							* </span>
							</label>

							<span class="btn blue fileinput-button" style="left: 90px;">
								<i class="fa fa-file" id="control1" name="control1"></i>
								<input type="file" id="cot1" name="cot1">
							</span>


							<a class="btn yellow" style="left: 120px;" data-toggle="modal" href="#valor" id="evaluador1" name="evaluador1"> Evaluar </a>
							<div class="col-md-3 proveedor2" style="left: -20px;">
								<select class="form-control input-xlarge select2me proveedor2" data-placeholder="Select..." name="p2" id="p2">
								
								</select>
								
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1">Proveedor 3
							</label>

							<span class="btn blue fileinput-button" style="left: 90px;">
								<i class="fa fa-file" id="control2" name="control2"></i>
								<input type="file" id="cot2" name="cot2">
							</span>
							
							<a class="btn yellow" style="left: 120px;" data-toggle="modal" href="#valor" id="evaluador2" name="evaluador2"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -20px;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p3" id="p3">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1">Proveedor 4
							</label>

							<span class="btn blue fileinput-button" style="left: 90px;">
								<i class="fa fa-file" id="control3" name="control3"></i>
								<input type="file" id="cot3" name="cot3">
							</span>
							
							<a class="btn yellow" style="left: 120px;" data-toggle="modal" href="#valor" id="evaluador3" name="evaluador3"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -20px;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p4" id="p4">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>

					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-1">Proveedor 5
							</label>
							
							<span class="btn blue fileinput-button" style="left: 90px;">
								<i class="fa fa-file" id="control4" name="control4"></i>
								<input type="file" id="cot4" name="cot4">
							</span>

							<a class="btn yellow" style="left: 120px;" data-toggle="modal" href="#valor" id="evaluador4" name="evaluador4"> Evaluar </a>
							<div class="col-md-3 proveedor3" style="left: -20px;">
								<select class="form-control input-xlarge select2me proveedor3" data-placeholder="Select..." name="p5" id="p5">
									<option value=""></option>
								</select>	
							</div>
						</div>
					</div>
					
					<?php
					}
				}
					?>


					<div id="responsive" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="380">
						<div class="modal-header">
							<button type="button" class="close" data-dismiss="modal" aria-hidden="true"></button>
							<h4 class="modal-title">Nuevo Proveedor</h4>
						</div>
						<div class="modal-body">
							<div class="row">
								<div class="col-md-12">
									<h4></h4>
									<p>
										<label>Nombre del Proveedor</label>
										<input class="form-control" type="text">
									</p>
									<p>
										<label>RUC</label>	
										<input class="form-control" type="text">
									</p>
									<p>
										<label>Dirección</label>
										<input class="form-control" type="text">
									</p>
									<p>
										<label>Persona de Contacto</label>
										<input class="form-control" type="text">
									</p>
									<p>
										<label>Teléfono</label>
										<input class="form-control" type="text">
									</p>
								</div>
							</div>
						</div>
						<div class="modal-footer">
							<button type="button" data-dismiss="modal" class="btn btn-default">Close</button>
							<button type="button" class="btn blue">Save changes</button>
						</div>
					</div>
					
					<div class="col-md-12">
						<div class="form-group">
							<label class="control-label col-md-2">Proveedor Sugerido<span class="required">
							* </span>
							</label>
							<div class="col-md-1 proveedore">
								<input type="text" style="text-align: center" class="form-control input-xlarge select2me proveedor" name="ps" id="ps" value="" readonly/>
							</div>

							<div class="col-md-1" style="left:320px;padding-top:5px;">
								<input type="checkbox" style="text-align: center; " onclick="captar();" class="md-check" name="psug"      id="psug"/><label>&nbsp;Otro</label>
							</div>

							<div class="col-md-1 proveedor" style="left:320px;">	
								<select type = "text" style="text-align: center" class="form-control input-xlarge select2me proveedor" data-placeholder="Select..." name="pe" id="pe" disabled>
									<option value=""></option>
								</select >	
							</div>
						</div>
						<input type="text" name="pelegido" id="pelegido" style="display:none;">
						<input type="text" name="cote" id="cote" style="display:none;">
						<input type="text" name="cote1" id="cote1" style="display:none;">
						<input type="text" name="cote2" id="cote2" style="display:none;">
						<input type="text" name="cote3" id="cote3" style="display:none;">
						<input type="text" name="cote4" id="cote4" style="display:none;">
					</div>

					<div class="col-md-12">
						<div class="form-group" style="text-align:center;">
							<div class="col-md-3" style="left:80px;top:30px;">
								<label>Comentario <span class="required" style="color:red">
							* </span></label>
							</div>
							<textarea placeholder="Comentario..." id="comentotro" name="comentotro" class="form-control" style="margin: 0px;width: 706px;height: 86px;" disabled></textarea>
						</div>
					</div>

				<div class="row">
					<div class="col-md-offset-5 col-md-8">
						<input type="submit" name="insert" position="center" class="btn btn-success" value="Registrar"> 	
					</div>
				</div>
			</form>

			<div class="form-actions">
				<div class="row-a">
					<div class="col-md-1" style="display:block;" id="atras2">
						<a href="javascript:;" class="btn blue button-previous" id="atras">
						<i class="m-icon-swapleft m-icon-white"></i></a>
					</div>
					<div class="col-md-1" style="display:none" id="siguiente2">				
						<a href="javascript:;" class="btn green button-next" id="siguiente">
						<i class="m-icon-swapright m-icon-white"></i>
						</a>
					</div>
					<div class="col-md-offset-1 col-md-9" style="display:none" id="fin2">
						<a href="javascript:;" class="btn yellow button-submit" id="fin">
						Finalizar <i class="m-icon-swapright m-icon-white"></i>  
						</a>
						
					</div>
				</div>
			</div>
			<?php
			}
		?>
	</div>

		<div class="tab-pane" id="tab4">
		<?php 
		while($rows = mysqli_fetch_array($resultado5a,MYSQLI_ASSOC) and $row = mysqli_fetch_array($resultado4a,MYSQLI_ASSOC))
		{
		if($rows['acepdoc']==""){ 

		?>	
				
				<form method="POST" id="formtab4" action="filedocumentacion.php" enctype="multipart/form-data" target="frame">
						<iframe name="frame" style="display:none"></iframe>
						<h4 class="block" style="padding-left: 40px;"><b>Documentación Solicitada</b></h4>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 2%;">
								<label><b>Nombre del Documento</b></label>
								</div>
								
								<div class="col-md-1 upload-btn-wrapper" style="left:6%;">

								  <label  style="text-transform: none;font-size: 14px;padding-left: 10%;padding-top:30px;border:none;background: transparent;"><b>Archivo</b></label>
								</div>

								<div class="col-md-1 upload-btn-wrapper" style="left:9%;">

								  <label  style="text-transform: none;font-size: 14px;padding-left: 12%;padding-top:30px;border:none;background: transparent;"><b>Sustento</b></label>
								</div>

								<div class="col-md-4 upload-btn-wrapper" style="left:18%;">

								  <label  style="text-transform: none;font-size: 14px;padding-left: 12%;padding-top:30px;border:none;background: transparent;"><b>Niveles de Aceptación de Requerimientos Mínimos</b></label>
								</div>

							</div>
							<hr>
						</div>
						<?php
						while($doc = mysqli_fetch_array($tbdoc,MYSQLI_ASSOC))
						{
						if($doc['evaluacionc'] == "Opcional"){
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Evaluación Crediticia</label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 62px;width: 112px;padding-left: 10px;padding-right: 10px;" id="estadob1" name="estadob1">Sin Documento</button>
								  <input type="file" name="eval" id="eval" />
								</div>
								<div class="col-md-1 upload-btn-wrapper">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="sestadob1" name="sestadob1">Sin Sustento</button>
								  <input type="file" name="seval" id="seval" />
								</div>

								<div class="col-md-6" style="left: 10%;padding-top: 1%;">
								<input type="radio" name="rdioec" id="inicial" value="" checked="checked" style="display:none;">
								<input type="radio" name="rdioec" id="conforme" value="Procede"> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioec" id="conobs" value="Procede Con Observación"> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioec" id="exocon" value="Exoneración con Conformidad"> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
								</div>
								
							</div>
						</div>
						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Evaluación Crediticia <span class="required" style="color:red">
							* </span></label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 62px;width: 112px;padding-left: 10px;padding-right: 10px;" id="estadob1" name="estadob1">Sin Documento</button>
								  <input type="file" name="eval" id="eval" required/>
								</div>
								<div class="col-md-1 upload-btn-wrapper">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="sestadob1" name="sestadob1">Sin Sustento</button>
								  <input type="file" name="seval" id="seval" />
								</div>

								<div class="col-md-6" style="left: 10%;padding-top: 1%;">
								<input type="radio" name="rdioec" id="inicial" value="" checked="checked" style="display:none;">
								<input type="radio" name="rdioec" id="conforme" value="Procede"> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioec" id="conobs" value="Procede Con Observación"> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioec" id="exocon" value="Exoneración con Conformidad"> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php	
						}
						if($doc['constanciana'] == "Obligatorio"){
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Constancia de No Adeudo<span class="required" style="color:red">
							* </span></label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 62px;width: 112px;padding-left: 10px;padding-right: 10px;" id="estadob2" name="estadob2">Sin Documento</button>
								  <input type="file" name="const" id="const" required/>
								</div>
								<div class="col-md-1 upload-btn-wrapper">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="sestadob2" name="sestadob2">Sin Sustento</button>
								  <input type="file" name="sconst" id="sconst" />
								</div>

								<div class="col-md-6" style="left: 10%;padding-top: 1%;">
								<input type="radio" name="rdiocna" id="inicial" value="" checked="checked" style="display:none;">	
								<input type="radio" name="rdiocna" id="conforme" value="Procede"> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiocna" id="conobs" value="Procede Con Observación"> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiocna" id="exocon" value="Exoneración con Conformidad"> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Constancia de No Adeudo</label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 62px;width: 112px;padding-left: 10px;padding-right: 10px;" id="estadob2" name="estadob2">Sin Documento</button>
								  <input type="file" name="const" id="const" />
								</div>
								<div class="col-md-1 upload-btn-wrapper">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="sestadob2" name="sestadob2">Sin Sustento</button>
								  <input type="file" name="sconst" id="sconst" />
								</div>

								<div class="col-md-6" style="left: 10%;padding-top: 1%;">
								<input type="radio" name="rdiocna" id="inicial" value="" checked="checked" style="display:none;">
								<input type="radio" name="rdiocna" id="conforme" value="Procede"> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiocna" id="conobs" value="Procede Con Observación"> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiocna" id="exocon" value="Exoneración con Conformidad"> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php	
						}
						if($doc['plaft'] == "Obligatorio"){
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>PLAFT<span class="required" style="color:red">
							* </span></label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 62px;width: 112px;padding-left: 10px;padding-right: 10px;" id="estadob3" name="estadob3">Sin Documento</button>
								  <input type="file" name="plaft" id="plaft" required/>
								</div>
								<div class="col-md-1 upload-btn-wrapper">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="sestadob3" name="sestadob3">Sin Sustento</button>
								  <input type="file" name="splaft" id="splaft" />
								</div>

								<div class="col-md-6" style="left: 10%;padding-top: 1%;">
								<input type="radio" name="rdioplaft" id="inicial" value="" checked="checked" style="display:none;">	
								<input type="radio" name="rdioplaft" id="conforme" value="Procede"> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioplaft" id="conobs" value="Procede Con Observación"> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioplaft" id="exocon" value="Exoneración con Conformidad"> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>PLAFT</label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 62px;width: 112px;padding-left: 10px;padding-right: 10px;" id="estadob3" name="estadob3">Sin Documento</button>
								  <input type="file" name="plaft" id="plaft" />
								</div>
								<div class="col-md-1 upload-btn-wrapper">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="sestadob3" name="sestadob3">Sin Sustento</button>
								  <input type="file" name="splaft" id="splaft" />
								</div>

								<div class="col-md-6" style="left: 10%;padding-top: 1%;">
								<input type="radio" name="rdioplaft" id="inicial" value="" checked="checked" style="display:none;">
								<input type="radio" name="rdioplaft" id="conforme" value="Procede"> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioplaft" id="conobs" value="Procede Con Observación"> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioplaft" id="exocon" value="Exoneración con Conformidad"> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php	
						}
						if($doc['sst'] == "Obligatorio"){
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>SST<span class="required" style="color:red">
							* </span></label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 62px;width: 112px;padding-left: 10px;padding-right: 10px;" id="estadob4" name="estadob4">Sin Documento</button>
								  <input type="file" name="sst" id="sst" required/>
								</div>
								<div class="col-md-1 upload-btn-wrapper">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="sestadob4" name="sestadob4">Sin Sustento</button>
								  <input type="file" name="ssst" id="ssst" />
								</div>

								<div class="col-md-6" style="left: 10%;padding-top: 1%;">
								<input type="radio" name="rdiosst" id="inicial" value="" checked="checked" style="display:none;">
								<input type="radio" name="rdiosst" id="conforme" value="Procede"> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiosst" id="conobs" value="Procede Con Observación"> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiosst" id="exocon" value="Exoneración con Conformidad"> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>

						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>SST</label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 62px;width: 112px;padding-left: 10px;padding-right: 10px;" id="estadob4" name="estadob4">Sin Documento</button>
								  <input type="file" name="sst" id="sst" />
								</div>
								<div class="col-md-1 upload-btn-wrapper">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="sestadob4" name="sestadob4">Sin Sustento</button>
								  <input type="file" name="ssst" id="ssst" />
								</div>

								<div class="col-md-6" style="left: 10%;padding-top: 1%;">
								<input type="radio" name="rdiosst" id="inicial" value="" checked="checked" style="display:none;">
								<input type="radio" name="rdiosst" id="conforme" value="Procede"> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiosst" id="conobs" value="Procede Con Observación"> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiosst" id="exocon" value="Exoneración con Conformidad"> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php	
						}
						if($doc['declaracionc'] == "Obligatorio"){
						?>

						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Declaración de Cumplimiento<span class="required" style="color:red">
							* </span></label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 62px;width: 112px;padding-left: 10px;padding-right: 10px;" id="estadob5" name="estadob5">Sin Documento</button>
								  <input type="file" name="cumpl" id="cumpl" required/>
								</div>
								<div class="col-md-1 upload-btn-wrapper">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="sestadob5" name="sestadob5">Sin Sustento</button>
								  <input type="file" name="scumpl" id="scumpl" />
								</div>

								<div class="col-md-6" style="left: 10%;padding-top: 1%;">
								<input type="radio" name="rdiodc" id="inicial" value="" checked="checked" style="display:none;">
								<input type="radio" name="rdiodc" id="conforme" value="Procede"> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiodc" id="conobs" value="Procede Con Observación"> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiodc" id="exocon" value="Exoneración con Conformidad"> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Declaración de Cumplimiento</label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 62px;width: 112px;padding-left: 10px;padding-right: 10px;" id="estadob5" name="estadob5">Sin Documento</button>
								  <input type="file" name="cumpl" id="cumpl" />
								</div>
								<div class="col-md-1 upload-btn-wrapper">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="sestadob5" name="sestadob5">Sin Sustento</button>
								  <input type="file" name="scumpl" id="scumpl" />
								</div>

								<div class="col-md-6" style="left: 10%;padding-top: 1%;">
								<input type="radio" name="rdiodc" id="inicial" value="" checked="checked" style="display:none;">
								<input type="radio" name="rdiodc" id="conforme" value="Procede"> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiodc" id="conobs" value="Procede Con Observación"> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiodc" id="exocon" value="Exoneración con Conformidad"> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php	
						}
						if($doc['homologacion'] == "Obligatorio"){
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Homologación<span class="required" style="color:red">
							* </span></label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 62px;width: 112px;padding-left: 10px;padding-right: 10px;" id="estadob6" name="estadob6">Sin Documento</button>
								  <input type="file" name="homo" id="homo" />
								</div>
								<div class="col-md-1 upload-btn-wrapper">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="sestadob6" name="sestadob6">Sin Sustento</button>
								  <input type="file" name="shomo" id="shomo" />
								</div>

								<div class="col-md-6" style="left: 10%;padding-top: 1%;">
								<input type="radio" name="rdioh" id="inicial" value="" checked="checked" style="display:none;">
								<input type="radio" name="rdioh" id="conforme" value="Procede"> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioh" id="conobs" value="Procede Con Observación"> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioh" id="exocon" value="Exoneración con Conformidad"> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Homologación</label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 62px;width: 112px;padding-left: 10px;padding-right: 10px;" id="estadob6" name="estadob6">Sin Documento</button>
								  <input type="file" name="homo" id="homo" />
								</div>
								<div class="col-md-1 upload-btn-wrapper">
								 <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px; padding-left: 15px;padding-right: 15px;" id="sestadob6" name="sestadob6">Sin Sustento</button>
								  <input type="file" name="shomo" id="shomo" />
								</div>

								<div class="col-md-6" style="left: 10%;padding-top: 1%;">
								<input type="radio" name="rdioh" id="inicial" value="" checked="checked" style="display:none;">
								<input type="radio" name="rdioh" id="conforme" value="Procede"> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioh" id="conobs" value="Procede Con Observación"> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioh" id="exocon" value="Exoneración con Conformidad"> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php
							}
						}
						?>
				<div class="row">
					<div class="col-md-offset-6 col-md-8">
						<input type="submit" name="upload" id="upload" position="center" class="btn btn-success" value="Enviar Documentación"> 	
					</div>
				</div>

						<input type="text" name="doc1" id="doc1" style="display:none;">
						<input type="text" name="doc2" id="doc2" style="display:none;">
						<input type="text" name="doc3" id="doc3" style="display:none;">
						<input type="text" name="doc4" id="doc4" style="display:none;">
						<input type="text" name="doc5" id="doc5" style="display:none;">
						<input type="text" name="doc6" id="doc6" style="display:none;">

						<input type="text" name="sdoc1" id="sdoc1" style="display:none;">
						<input type="text" name="sdoc2" id="sdoc2" style="display:none;">
						<input type="text" name="sdoc3" id="sdoc3" style="display:none;">
						<input type="text" name="sdoc4" id="sdoc4" style="display:none;">
						<input type="text" name="sdoc5" id="sdoc5" style="display:none;">
						<input type="text" name="sdoc6" id="sdoc6" style="display:none;">

				</form>
			<div class="form-actions">
				<div class="row-a">
					<div class="col-md-1" style="display:block;" id="atras3">
						<a href="javascript:;" class="btn blue button-previous" id="atras">
						<i class="m-icon-swapleft m-icon-white"></i></a>
					</div>
					<div class="col-md-1" style="display:none" id="siguiente3">				
						<a href="javascript:;" class="btn green button-next" id="siguiente">
						<i class="m-icon-swapright m-icon-white"></i>
						</a>
					</div>
					<div class="col-md-offset-1 col-md-9" style="display:none" id="fin3">
						<a href="javascript:;" class="btn yellow button-submit" id="fin">
						Finalizar <i class="m-icon-swapright m-icon-white"></i>  
						</a>
						
					</div>
				</div>
						
			</div>
		<?php 
		}elseif($rows['acepdoc']=="no"){ 
		?>	
			<form method="POST" id="formtab4" action="filedocumentacion.php" enctype="multipart/form-data" target="frame">
						<iframe name="frame" style="display:none"></iframe>
						<h4 class="block" style="padding-left: 40px;"><b>Documentación Solicitada</b></h4>
						<?php
						while($doc = mysqli_fetch_array($tbdoc,MYSQLI_ASSOC) and $docprov = mysqli_fetch_array($docproveedor,MYSQLI_ASSOC))
						{
						if($doc['evaluacionc'] == "Opcional"){

						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 150px;padding-top: 30px;">
								<label>Evaluación Crediticia</label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:80px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadob1" name="estadob1">Agregar nueva versión</button>
								  <input type="file" name="eval" id="eval" />
								</div>
								<?php if ($docprov['eval'] == ""){
								} else
								{
								?>
								<a href="descargad.php?archivo=<?php echo $docprov['eval'];?>" style="left: 90px;top:20px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Versión anterior</a>
								<?php 
								}
								?>
								<div class="col-md-6" style="left: 150px;padding-top: 1%;">
								<input type="radio" name="rdioec" id="conforme" value="Conforme"> Conforme&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioec" id="conobs" value="Con Observación"> Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioec" id="exocon" value="Exoneración con conformidad"> Exoneración con conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 150px;padding-top: 30px;">
								<label>Evaluación Crediticia <span class="required">
							* </span></label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:80px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadob1" name="estadob1">Agregar nueva versión</button>
								  <input type="file" name="eval" id="eval" required/>
								</div>
								<?php if ($docprov['eval'] == ""){
								} else
								{
								?>
								<a href="descargad.php?archivo=<?php echo $docprov['eval'];?>" style="left: 90px;top:20px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Versión anterior</a>
								<?php 
								}
								?>
								<div class="col-md-6" style="left: 150px;padding-top: 1%;">
								<input type="radio" name="rdioec" id="conforme" value="Conforme"> Conforme&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioec" id="conobs" value="Con Observación"> Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioec" id="exocon" value="Exoneración con conformidad"> Exoneración con conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php	
						}
						if($doc['constanciana'] == "Obligatorio"){
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 150px;padding-top: 30px;">
								<label>Constancia de No Adeudo<span class="required" style="color:red">
							* </span></label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:80px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadob2" name="estadob2">Agregar nueva versión</button>
								  <input type="file" name="const" id="const" required/>
								</div>
								<?php if ($docprov['const'] == ""){
								} else
								{
								?>
								<a href="descargad.php?archivo=<?php echo $docprov['const'];?>" style="left: 90px;top:20px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Versión anterior</a>
								<?php 
								}
								?>
								<div class="col-md-6" style="left: 150px;padding-top: 1%;">
								<input type="radio" name="rdiocn" id="conforme" value="Conforme"> Conforme&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiocn" id="conobs" value="Con Observación"> Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiocn" id="exocon" value="Exoneración con conformidad"> Exoneración con conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 150px;padding-top: 30px;">
								<label>Constancia de No Adeudo</label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:80px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadob2" name="estadob2">Agregar nueva versión</button>
								  <input type="file" name="const" id="const" />
								</div>

								<?php if ($docprov['const']==""){
								} else
								{
								?>
								<a href="descargad.php?archivo=<?php echo $docprov['const'];?>" style="left: 90px;top:20px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Versión anterior</a>
								<?php 
								}
								?>
								<div class="col-md-6" style="left: 150px;padding-top: 1%;">
								<input type="radio" name="rdiocn" id="conforme" value="Conforme"> Conforme&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiocn" id="conobs" value="Con Observación"> Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiocn" id="exocon" value="Exoneración con conformidad"> Exoneración con conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php	
						}
						if($doc['plaft'] == "Obligatorio"){
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 150px;padding-top: 30px;">
								<label>PLAFT<span class="required" style="color:red">
							* </span></label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:80px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadob3" name="estadob3">Agregar nueva versión</button>
								  <input type="file" name="plaft" id="plaft" required/>
								</div>
								<?php if ($docprov['plaft'] == ""){
								} else
								{
								?>
								<a href="descargad.php?archivo=<?php echo $docprov['plaft'];?>" style="left: 90px;top:20px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Versión anterior</a>
								<?php 
								}
								?>
								<div class="col-md-6" style="left: 150px;padding-top: 1%;">
								<input type="radio" name="rdiop" id="conforme" value="Conforme"> Conforme&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiop" id="conobs" value="Con Observación"> Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiop" id="exocon" value="Exoneración con conformidad"> Exoneración con conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 150px;padding-top: 30px;">
								<label>PLAFT</label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:80px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadob3" name="estadob3">Agregar nueva versión</button>
								  <input type="file" name="plaft" id="plaft" />
								</div>

								<?php if ($docprov['plaft'] == ""){
								} else
								{
								?>
								<a href="descargad.php?archivo=<?php echo $docprov['plaft'];?>" style="left: 90px;top:20px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Versión anterior</a>
								<?php 
								}
								?>
								<div class="col-md-6" style="left: 150px;padding-top: 1%;">
								<input type="radio" name="rdiop" id="conforme" value="Conforme"> Conforme&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiop" id="conobs" value="Con Observación"> Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiop" id="exocon" value="Exoneración con conformidad"> Exoneración con conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php	
						}
						if($doc['sst'] == "Obligatorio"){
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 150px;padding-top: 30px;">
								<label>SST<span class="required" style="color:red">
							* </span></label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:80px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadob4" name="estadob4">Agregar nueva versión</button>
								  <input type="file" name="sst" id="sst" required/>
								</div>

								<?php if ($docprov['sst'] == ""){
								} else
								{
								?>
								<a href="descargad.php?archivo=<?php echo $docprov['sst'];?>" style="left: 90px;top:20px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Versión anterior</a>
								<?php 
								}
								?>
								<div class="col-md-6" style="left: 150px;padding-top: 1%;">
								<input type="radio" name="rdioss" id="conforme" value="Conforme"> Conforme&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioss" id="conobs" value="Con Observación"> Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioss" id="exocon" value="Exoneración con conformidad"> Exoneración con conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>

						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 150px;padding-top: 30px;">
								<label>SST</label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:80px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadob4" name="estadob4">Agregar nueva versión</button>
								  <input type="file" name="sst" id="sst" />
								</div>

								<?php if ($docprov['sst'] == ""){
								} else
								{
								?>
								<a href="descargad.php?archivo=<?php echo $docprov['sst'];?>" style="left: 90px;top:20px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Versión anterior</a>
								<?php 
								}
								?>
								<div class="col-md-6" style="left: 150px;padding-top: 1%;">
								<input type="radio" name="rdioss" id="conforme" value="Conforme"> Conforme&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioss" id="conobs" value="Con Observación"> Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioss" id="exocon" value="Exoneración con conformidad"> Exoneración con conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php	
						}
						if($doc['declaracionc'] == "Obligatorio"){
						?>

						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 150px;padding-top: 30px;">
								<label>Declaración de Cumplimiento<span class="required" style="color:red">
							* </span></label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:80px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadob5" name="estadob5">Agregar nueva versión</button>
								  <input type="file" name="cumpl" id="cumpl" required/>
								</div>

								<?php if ($docprov['cumpl'] == ""){
								} else
								{
								?>
								<a href="descargad.php?archivo=<?php echo $docprov['cumpl'];?>" style="left: 90px;top:20px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Versión anterior</a>
								<?php 
								}
								?>
								<div class="col-md-6" style="left: 150px;padding-top: 1%;">
								<input type="radio" name="rdiodc" id="conforme" value="Conforme"> Conforme&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiodc" id="conobs" value="Con Observación"> Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiodc" id="exocon" value="Exoneración con conformidad"> Exoneración con conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 150px;padding-top: 30px;">
								<label>Declaración de Cumplimiento</label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:80px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadob5" name="estadob5">Agregar nueva versión</button>
								  <input type="file" name="cumpl" id="cumpl" />
								</div>

								<?php if ($docprov['cumpl'] == ""){
								} else
								{
								?>
								<a href="descargad.php?archivo=<?php echo $docprov['cumpl'];?>" style="left: 90px;top:20px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Versión anterior</a>
								<?php 
								}
								?>
								<div class="col-md-6" style="left: 150px;padding-top: 1%;">
								<input type="radio" name="rdiodc" id="conforme" value="Conforme"> Conforme&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiodc" id="conobs" value="Con Observación"> Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdiodc" id="exocon" value="Exoneración con conformidad"> Exoneración con conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php	
						}
						if($doc['homologacion'] == "Obligatorio"){
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 150px;padding-top: 30px;">
								<label>Homologación<span class="required" style="color:red">
							* </span></label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:80px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadob6" name="estadob6">Agregar nueva versión</button>
								  <input type="file" name="homo" id="homo" />
								</div>

								<?php if ($docprov['homo'] == ""){
								} else
								{
								?>
								<a href="descargad.php?archivo=<?php echo $docprov['homo'];?>" style="left: 90px;top:20px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Versión anterior</a>
								<?php 
								}
								?>
								<div class="col-md-6" style="left: 150px;padding-top: 1%;">
								<input type="radio" name="rdioh" id="conforme" value="Conforme"> Conforme&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioh" id="conobs" value="Con Observación"> Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioh" id="exocon" value="Exoneración con conformidad"> Exoneración con conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Homologación</label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadob6" name="estadob6">Agregar nueva versión</button>
								  <input type="file" name="homo" id="homo" />
								</div>

								<?php if ($docprov['homo'] == ""){
								} else
								{
								?>
								<a href="descargad.php?archivo=<?php echo $docprov['homo'];?>" style="left: 90px;top:20px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i>Versión anterior</a>
								<?php 
								}
								?>
								<div class="col-md-6" style="left: 150px;padding-top: 1%;">
								<input type="radio" name="rdioh" id="conforme" value="Conforme"> Conforme&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioh" id="conobs" value="Con Observación"> Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
								<input type="radio" name="rdioh" id="exocon" value="Exoneración con conformidad"> Exoneración con conformidad&nbsp;&nbsp;&nbsp;
								</div>
							</div>
						</div>
						<?php
							}
						}
						?>
						<div class="row">
					<div class="col-md-offset-6 col-md-8">
						<input type="submit" name="upload" id="upload" position="center" class="btn btn-success" value="Actualizar Documentación"> 	
					</div>
				</div>

						<input type="text" name="doc1" id="doc1" style="display:none;">
						<input type="text" name="doc2" id="doc2" style="display:none;">
						<input type="text" name="doc3" id="doc3" style="display:none;">
						<input type="text" name="doc4" id="doc4" style="display:none;">
						<input type="text" name="doc5" id="doc5" style="display:none;">
						<input type="text" name="doc6" id="doc6" style="display:none;">

					</form>
					<div class="form-actions">
				<div class="row-a">
					<div class="col-md-1" style="display:block;" id="atras3">
						<a href="javascript:;" class="btn blue button-previous" id="atras">
						<i class="m-icon-swapleft m-icon-white"></i></a>
					</div>
					<div class="col-md-1" style="display:none" id="siguiente3">				
						<a href="javascript:;" class="btn green button-next" id="siguiente">
						<i class="m-icon-swapright m-icon-white"></i>
						</a>
					</div>
					<div class="col-md-offset-1 col-md-9" style="display:none" id="fin3">
						<a href="javascript:;" class="btn yellow button-submit" id="fin">
						Finalizar <i class="m-icon-swapright m-icon-white"></i>  
						</a>
						
					</div>
				</div>
			</div>
		<?php 
		} else{ 
		?>
			<h4 class="block" style="padding-left: 40px;"><b>Documentación Solicitada</b></h4>
				<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 2%;">
								<label><b>Nombre del Documento</b></label>
								</div>
								
								<div class="col-md-1 upload-btn-wrapper" style="left:6%;">

								  <label  style="text-transform: none;font-size: 14px;padding-left: 10%;padding-top:30px;border:none;background: transparent;"><b>Archivo</b></label>
								</div>

								<div class="col-md-1 upload-btn-wrapper" style="left:9%;">

								  <label  style="text-transform: none;font-size: 14px;padding-left: 12%;padding-top:30px;border:none;background: transparent;"><b>Sustento</b></label>
								</div>

								<div class="col-md-4 upload-btn-wrapper" style="left:18%;">

								  <label  style="text-transform: none;font-size: 14px;padding-left: 12%;padding-top:30px;border:none;background: transparent;"><b>Niveles de Aceptación de Requerimientos Mínimos</b></label>
								</div>

							</div>
							<hr>
						</div>
				<?php
				while($doc = mysqli_fetch_array($tbdoca,MYSQLI_ASSOC) and $docprov = mysqli_fetch_array($docproveedora,MYSQLI_ASSOC) and $docsust = mysqli_fetch_array($docsustentosa,MYSQLI_ASSOC))
				{
				if($doc['evaluacionc'] == "Opcional"){

				?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Evaluación Crediticia</label>
								</div>

								<?php if ($docprov['eval'] == ""){?>
									<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;padding-top:10px;width:112px">No aplica</button>
								</div>
										<?php if ($docsust['seval'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											  
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioeca" id="inicial" value="" checked="checked" style="display:none;">
											<input type="radio" name="rdioeca" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioeca" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioeca" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>	
											<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['seval'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>
											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioeca" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioeca" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioeca" id="exocon" value="Exoneración con Conformidad" checked="checked" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
											<?php 
										}
											?>
								<?php

								} else
								{
								?>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  
								  <a href="descargad.php?archivo=<?php echo $docprov['eval'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

								</div>
										<?php if ($docsust['seval'] == ""){?>
										<div class="col-md-1 upload-btn-wrapper">
										  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
										
										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioeca" id="conforme" value="Procede" checked="checked" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioeca" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioeca" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>

										<?php

										} else
										{
										?>

										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['seval'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioeca" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioeca" id="conobs" value="Procede Con Observación" checked="checked" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioeca" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php
										}
										?>

								<?php 
								}
								?>

							</div>
						</div>
						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Evaluación Crediticia <span class="required" style="color:red">
							* </span></label>
								</div>
								
								<?php if ($docprov['eval'] == ""){?>
									<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;padding-top:10px;padding-left: 10px;padding-right: 10px;">Sin Documento</button>
								</div>
										<?php if ($docsust['seval'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											  
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioeca" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioeca" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioeca" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>
										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['seval'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>
										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioeca" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioeca" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioeca" id="exocon" value="Exoneración con Conformidad" checked="checked" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php 
										}?>
								<?php
								} else
								{
								?>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								<a href="descargad.php?archivo=<?php echo $docprov['eval'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>
								</div>

								<?php if ($docsust['seval'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											  
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioeca" id="conforme" value="Procede" checked="checked" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioeca" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioeca" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>
										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['seval'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioeca" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioeca" id="conobs" value="Procede Con Observación" checked="checked" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioeca" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php 
								}
								?>

								<?php 
								}
								?>
								
							</div>
						</div>
						<?php	
						}
						if($doc['constanciana'] == "Opcional"){

				?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Constancia de No Adeudo</label>
								</div>

								<?php if ($docprov['const'] == ""){?>
									<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;padding-top:10px;width:112px">No aplica</button>
								</div>
										<?php if ($docsust['scna'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											  
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecas" id="inicial" value="" checked="checked" style="display:none;">
											<input type="radio" name="rdioecas" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecas" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecas" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>	
											<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['scna'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>
											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioeca" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioeca" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioeca" id="exocon" value="Exoneración con Conformidad" checked="checked" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
											<?php 
										}
											?>
								<?php

								} else
								{
								?>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  
								  <a href="descargad.php?archivo=<?php echo $docprov['const'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

								</div>
										<?php if ($docsust['scna'] == ""){?>
										<div class="col-md-1 upload-btn-wrapper">
										  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
										 
										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioeca" id="conforme" value="Procede" checked="checked" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioeca" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioeca" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>

										<?php

										} else
										{
										?>

										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['scna'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioeca" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioeca" id="conobs" value="Procede Con Observación" checked="checked" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioeca" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php
										}
										?>

								<?php 
								}
								?>

							</div>
						</div>
						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Constancia de No Adeudo <span class="required" style="color:red">
							* </span></label>
								</div>
								
								<?php if ($docprov['const'] == ""){?>
									<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;padding-top:10px;padding-left: 10px;padding-right: 10px;">Sin Documento</button>
								</div>
										<?php if ($docsust['scna'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecas" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecas" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecas" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>
										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['scna'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>
										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecas" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecas" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecas" id="exocon" value="Exoneración con Conformidad" checked="checked" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php 
										}?>
								<?php
								} else
								{
								?>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								<a href="descargad.php?archivo=<?php echo $docprov['const'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>
								</div>

								<?php if ($docsust['scna'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											  
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecas" id="conforme" value="Procede" checked="checked" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecas" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecas" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>
										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['scna'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecas" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecas" id="conobs" value="Procede Con Observación" checked="checked" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecas" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php 
								}
								?>

								<?php 
								}
								?>
								
							</div>
						</div>
						<?php	
						}
						if($doc['plaft'] == "Opcional"){

				?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>PLAFT</label>
								</div>

								<?php if ($docprov['plaft'] == ""){?>
									<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;padding-top:10px;width:112px">No aplica</button>
								</div>
										<?php if ($docsust['splaft'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											  
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecasa" id="inicial" value="" checked="checked" style="display:none;">
											<input type="radio" name="rdioecasa" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasa" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasa" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>	
											<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['splaft'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>
											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecasa" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasa" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasa" id="exocon" value="Exoneración con Conformidad" checked="checked" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
											<?php 
										}
											?>
								<?php

								} else
								{
								?>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  
								  <a href="descargad.php?archivo=<?php echo $docprov['plaft'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

								</div>
										<?php if ($docsust['splaft'] == ""){?>
										<div class="col-md-1 upload-btn-wrapper">
										  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
										 
										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecasa" id="conforme" value="Procede" checked="checked" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasa" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasa" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>

										<?php

										} else
										{
										?>

										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['splaft'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecasa" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasa" id="conobs" value="Procede Con Observación" checked="checked" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasa" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php
										}
										?>

								<?php 
								}
								?>

							</div>
						</div>
						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>PLAFT <span class="required" style="color:red">
							* </span></label>
								</div>
								
								<?php if ($docprov['plaft'] == ""){?>
									<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;padding-top:10px;padding-left: 10px;padding-right: 10px;">Sin Documento</button>
								</div>
										<?php if ($docsust['splaft'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecasa" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasa" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasa" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>
										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['splaft'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>
										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecasa" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasa" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasa" id="exocon" value="Exoneración con Conformidad" checked="checked" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php 
										}?>
								<?php
								} else
								{
								?>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								<a href="descargad.php?archivo=<?php echo $docprov['plaft'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>
								</div>

								<?php if ($docsust['splaft'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											  
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecasa" id="conforme" value="Procede" checked="checked" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasa" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasa" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>
										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['splaft'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecasa" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasa" id="conobs" value="Procede Con Observación" checked="checked" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasa" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php 
								}
								?>

								<?php 
								}
								?>
								
							</div>
						</div>
						<?php	
						}
						if($doc['sst'] == "Opcional"){

				?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>SST</label>
								</div>

								<?php if ($docprov['sst'] == ""){?>
									<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;padding-top:10px;width:112px">No aplica</button>
								</div>
										<?php if ($docsust['ssst'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											  
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecasas" id="inicial" value="" checked="checked" style="display:none;">
											<input type="radio" name="rdioecasas" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasas" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasas" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>	
											<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['ssst'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>
											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecasas" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasas" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasas" id="exocon" value="Exoneración con Conformidad" checked="checked" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
											<?php 
										}
											?>
								<?php

								} else
								{
								?>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  
								  <a href="descargad.php?archivo=<?php echo $docprov['sst'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

								</div>
										<?php if ($docsust['ssst'] == ""){?>
										<div class="col-md-1 upload-btn-wrapper">
										  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
										 
										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecasas" id="conforme" value="Procede" checked="checked" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasas" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasas" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>

										<?php

										} else
										{
										?>

										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['ssst'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecasas" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasas" id="conobs" value="Procede Con Observación" checked="checked" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasas" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php
										}
										?>

								<?php 
								}
								?>

							</div>
						</div>
						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>SST<span class="required" style="color:red">
							* </span></label>
								</div>
								
								<?php if ($docprov['sst'] == ""){?>
									<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;padding-top:10px;width:112px;padding-left: 10px;padding-right: 10px;">Sin Documento</button>
								</div>
										<?php if ($docsust['ssst'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecasas" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasas" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasas" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>
										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['ssst'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>
										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecasas" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasas" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasas" id="exocon" value="Exoneración con Conformidad" checked="checked" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php 
										}?>
								<?php
								} else
								{
								?>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								<a href="descargad.php?archivo=<?php echo $docprov['sst'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>
								</div>

								<?php if ($docsust['ssst'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											 
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecasas" id="conforme" value="Procede" checked="checked" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasas" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasas" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>
										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['ssst'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecasas" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasas" id="conobs" value="Procede Con Observación" checked="checked" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasas" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php 
								}
								?>

								<?php 
								}
								?>
								
							</div>
						</div>
						<?php	
						}
						if($doc['declaracionc'] == "Opcional"){

				?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Declaración de Cumplimiento</label>
								</div>

								<?php if ($docprov['cumpl'] == ""){?>
									<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;padding-top:10px;width:112px">No aplica</button>
								</div>
										<?php if ($docsust['sdc'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											  
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecasasa" id="inicial" value="" checked="checked" style="display:none;">
											<input type="radio" name="rdioecasasa" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasasa" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasasa" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>	
											<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['sdc'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>
											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecasasa" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasasa" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasasa" id="exocon" value="Exoneración con Conformidad" checked="checked" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
											<?php 
										}
											?>
								<?php

								} else
								{
								?>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  
								  <a href="descargad.php?archivo=<?php echo $docprov['cumpl'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

								</div>
										<?php if ($docsust['sdc'] == ""){?>
										<div class="col-md-1 upload-btn-wrapper">
										  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
										 
										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecasasa" id="conforme" value="Procede" checked="checked" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasasa" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasasa" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>

										<?php

										} else
										{
										?>

										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['sdc'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecasasa" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasasa" id="conobs" value="Procede Con Observación" checked="checked" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasasa" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php
										}
										?>

								<?php 
								}
								?>

							</div>
						</div>
						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Declaración de Cumplimiento<span class="required" style="color:red">
							* </span></label>
								</div>
								
								<?php if ($docprov['cumpl'] == ""){?>
									<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;padding-top:10px;width:112px;padding-left: 10px;padding-right: 10px;">Sin Documento</button>
								</div>
										<?php if ($docsust['sdc'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecasasa" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasasa" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasasa" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>
										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['sdc'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>
										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecasasa" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasasa" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasasa" id="exocon" value="Exoneración con Conformidad" checked="checked" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php 
										}?>
								<?php
								} else
								{
								?>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								<a href="descargad.php?archivo=<?php echo $docprov['cumpl'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>
								</div>

								<?php if ($docsust['sdc'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											  
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecasasa" id="conforme" value="Procede" checked="checked" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasasa" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasasa" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>
										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['sdc'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecasasa" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasasa" id="conobs" value="Procede Con Observación" checked="checked" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasasa" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php 
								}
								?>

								<?php 
								}
								?>
								
							</div>
						</div>
						<?php	
						}
						if($doc['homologacion'] == "Opcional"){

				?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Homologación</label>
								</div>

								<?php if ($docprov['homo'] == ""){?>
									<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;padding-top:10px;width:112px">No aplica</button>
								</div>
										<?php if ($docsust['shomo'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											  
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecasasas" id="inicial" value="" checked="checked" style="display:none;">
											<input type="radio" name="rdioecasasas" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasasas" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasasas" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>	
											<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['shomo'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>
											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecasasas" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasasas" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasasas" id="exocon" value="Exoneración con Conformidad" checked="checked" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
											<?php 
										}
											?>
								<?php

								} else
								{
								?>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  
								  <a href="descargad.php?archivo=<?php echo $docprov['homo'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

								</div>
										<?php if ($docsust['shomo'] == ""){?>
										<div class="col-md-1 upload-btn-wrapper">
										  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
										 
										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecasasas" id="conforme" value="Procede" checked="checked" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasasas" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasasas" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>

										<?php

										} else
										{
										?>

										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['shomo'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecasasas" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasasas" id="conobs" value="Procede Con Observación" checked="checked" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasasas" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php
										}
										?>

								<?php 
								}
								?>

							</div>
						</div>
						<?php 
						}else{
						?>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 1%;">
								<label>Homologación<span class="required" style="color:red">
							* </span></label>
								</div>
								
								<?php if ($docprov['homo'] == ""){?>
									<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;padding-top:10px;width:112px;padding-left: 10px;padding-right: 10px;">Sin Documento</button>
								</div>
										<?php if ($docsust['shomo'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecasasas" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasasas" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasasas" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>
										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['shomo'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>
										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecasasas" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasasas" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasasas" id="exocon" value="Exoneración con Conformidad" checked="checked" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php 
										}?>
								<?php
								} else
								{
								?>
								<div class="col-md-2 upload-btn-wrapper" style="left:6%;padding-left:0%">
								<a href="descargad.php?archivo=<?php echo $docprov['homo'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>
								</div>

								<?php if ($docsust['shomo'] == ""){?>
											<div class="col-md-1 upload-btn-wrapper">
											  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;width:112px;padding-left: 15px;padding-right: 15px;" id="estadob1" name="estadob1">Sin Sustento</button>
											  
											</div>

											<div class="col-md-6" style="left: 10%;padding-top: 1%;">
											<input type="radio" name="rdioecasasas" id="conforme" value="Procede" checked="checked" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasasas" id="conobs" value="Procede Con Observación" disabled> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
											<input type="radio" name="rdioecasasas" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
											</div>
										<?php

										} else
										{
										?>
										<div class="col-md-1 upload-btn-wrapper">
										  
										  <a href="descargad.php?archivo=<?php echo $docsust['shomo'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="seval" name="seval"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar</a>

										</div>

										<div class="col-md-6" style="left: 10%;padding-top: 1%;">
										<input type="radio" name="rdioecasasas" id="conforme" value="Procede" disabled> Procede&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasasas" id="conobs" value="Procede Con Observación" checked="checked" disabled="disabled"> Procede Con Observación&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
										<input type="radio" name="rdioecasasas" id="exocon" value="Exoneración con Conformidad" disabled> Exoneración con Conformidad&nbsp;&nbsp;&nbsp;
										</div>
										<?php 
								}
								?>

								<?php 
								}
								?>
								
							</div>
						</div>
						<?php	
						}
					}
						?>
				
			<div class="form-actions">
				<div class="row-a">
					<div class="col-md-1" style="display:block;" id="atras3">
						<a href="javascript:;" class="btn blue button-previous" id="atras">
						<i class="m-icon-swapleft m-icon-white"></i></a>
					</div>
					<div class="col-md-1" style="display:block;float: right;" id="siguiente3">				
						<a href="javascript:;" class="btn green button-next" id="siguiente">
						<i class="m-icon-swapright m-icon-white"></i>
						</a>
					</div>
					<div class="col-md-offset-1 col-md-9" style="display:none" id="fin3">
						<a href="javascript:;" class="btn yellow button-submit" id="fin">
						Finalizar <i class="m-icon-swapright m-icon-white"></i>  
						</a>
						
					</div>
				</div>
			</div>
		<?php 
			}
		}
		?>

		</div>

				<div class="tab-pane" id="tab5">
					<form method="POST" id="formtab5" action="insert.php" enctype="multipart/from-data">
						<h4 class="block" ><b>Evaluación de Riesgos</b></h4>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-2" style="height:120px; left: 90px;padding-top:70px;">
								<label>Riesgo Operativo</label>
								</div>
								<div class="col-md-7" style="left:40px;">
								<textarea style="margin: 0px; width: 665px; height: 157px;"></textarea>
								</div>
							</div>
						</div>

						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-2" style="height:120px; left: 90px;padding-top:70px;">
								<label>Continuidad del Negocio</label>
								</div>
								<div class="col-md-7" style="left:40px;">
								<textarea style="margin: 0px; width: 665px; height: 157px;"></textarea>
								</div>
							</div>
						</div>

						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-2" style="height:120px; left: 90px;padding-top:70px;">
								<label>Seguridad de la Información</label>
								</div>
								<div class="col-md-7" style="left:40px;">
								<textarea style="margin: 0px; width: 665px; height: 157px;"></textarea>
								</div>
							</div>
						</div>

						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-2" style="height:120px; left: 90px;padding-top:70px;">
								<label>Niveles de servicio</label>
								</div>
								<div class="col-md-7" style="left:40px;">
								<textarea style="margin: 0px; width: 665px; height: 157px;"></textarea>
								</div>
							</div>
						</div>

						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-2" style="left: 90px;">
								<label>Informe Final</label>
								</div>
								<div class="col-md-7" style="left:40px;">
								<input type="file">
								</div>
							</div>
						</div>

					</form>
					<div class="form-actions">
						<div class="row-a">
							<div class="col-md-1" style="display:block;" id="atras4">
								<a href="javascript:;" class="btn blue button-previous" id="atras">
								<i class="m-icon-swapleft m-icon-white"></i></a>
							</div>
							<div class="col-md-1" style="display:block;float: right;" id="siguiente4">				
								<a href="javascript:;" class="btn green button-next" id="siguiente">
								<i class="m-icon-swapright m-icon-white"></i>
								</a>
							</div>
							<div class="col-md-offset-1 col-md-9" style="display:none" id="fin2">
								<a href="javascript:;" class="btn yellow button-submit" id="fin">
								Finalizar <i class="m-icon-swapright m-icon-white"></i>  
								</a>
								
							</div>
						</div>
					</div>
				</div>

				<div class="tab-pane" id="tab6">
				<?php 
				while($rows = mysqli_fetch_array($contrato,MYSQLI_ASSOC) and $ccc =mysqli_fetch_array($estado,MYSQLI_ASSOC) and $ddd =mysqli_fetch_array($requeridoc,MYSQLI_ASSOC) )
				{
				if($rows['acepcont']==""){ 
				?>	
					<form method="POST" id="formtab6" action="fileup.php" enctype="multipart/form-data" target="frame">
						<iframe name="frame" style="display:none"></iframe>
						<h4 class="block" ><b>Contratos</b></h4>
						<div class="col-md-4">
							<div class="form-group">
								
								<?php 
								 if ($ddd['contrato']=="Obligatorio") {		
								 ?>
								 <div class="col-md-4" style="left: 10%;padding-top: 30px;">
								<label>Contrato<span style="color:red;">*</span></label>
								<?php 
								 }else {		
								 ?>
								 <div class="col-md-4" style="left: 18%;padding-top: 30px;">
								<label>Orden de Compra<span style="color:red;">*</span></label>
								<?php 
								 }		
								 ?>
								</div>

								
								  <?php 
								  if ($ddd['contrato']=="Obligatorio") {		
								  ?>
								  <div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;" id="estadob" name="estadob">Sin Documento</button>
								  <input type="file" name="contrato1" id="contrato1"required/>
								  <?php 
								  }else {		
								  ?>
								  <div class="col-md-2 upload-btn-wrapper" style="left:21%;top:12px;width: 225px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;" id="estadob" name="estadob">Sin Documento</button>
								  <input type="file" name="contrato1" id="contrato1" required/>
								  <?php 
								  }		
								  ?>
								</div>
								<a class="btn blue" style="left: 86%;margin-top:-11%;" onclick="clausula()">Ver Clausulas</a>
								  <input type="text" name="contra" id="contra" style="display:none;">

							</div>
						</div>
						<?php 
							if ($ddd['contrato']=="Obligatorio") {		
						?>
						<div class="col-md-4">
							<div class="form-group">
								 <div class="col-md-4" style="left: 10%;padding-top: 30px;">
								  	<label>Ficha RUC<span style="color:red;">*</span></label>
								</div>

								  <div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;" id="estadofruc" name="estadofruc">No hay documento cargado</button>
								  <input type="file" name="fruc" id="fruc" required/>
								</div>
								 <input type="text" name="dfruc" id="dfruc" style="display:none;">
							</div>
						</div>
						<div class="col-md-4">
							<div class="form-group">
								 <div class="col-md-4" style="left: 10%;padding-top: 30px;">
								  	<label>DNI de quien firma<span style="color:red;">*</span></label>
								</div>

								 <div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;" id="estadodnif" name="estadodnif">No hay documento cargado</button>
								  <input type="file" name="dnif" id="dnif" required/>
								</div>
								 <input type="text" name="ddnif" id="ddnif" style="display:none;">
							</div>
						</div>
						<div class="col-md-4">
							<div class="form-group">
								 <div class="col-md-4" style="left: 10%;padding-top: 30px;">
								  	<label>Constancia de No Adeudo<span style="color:red;">*</span></label>
								</div>

								 <div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;" id="estadocnadeudo" name="estadocnadeudo">No hay documento cargado</button>
								  <input type="file" name="cnadeudo" id="cnadeudo" required/>
								</div>
								 <input type="text" name="dcnadeudo" id="dcnadeudo" style="display:none;">
								 
							</div>
						</div>
						<div class="col-md-4">
							<div class="form-group">
								 <div class="col-md-4" style="left: 10%;padding-top: 30px;">
								  	<label>Vigencia de Poder<span style="color:red;">*</span></label>
								</div>

								 <div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 60px;" id="estadovpoder" name= "estadovpoder">No hay documento cargado</button>
								  <input type="file" name="vpoder" id="vpoder" required/>
								</div>
								 <input type="text" name="dvpoder" id="dvpoder" style="display:none;">
							</div>

						</div>

						<div class="col-md-4">
							<div class="form-group">
								<div class="col-md-4" style="left: 10%;padding-top: 30px;">
								<label>Plantillas</label>
								</div>
								<div class="col-md-2" style="left:10%;top:12px;width: 225px;">
									<select  class="form-control input select2m" data-placeholder="Select..." name="archivo" id="archivo">
										<option value="" selected></option>
										<option value="modelodb.xlsx">modelodb</option>
										<option value="FALSE.xlsx">falso</option>
										<option value="Copia de CamposProveedores (2).xlsx">proveedor</option>
										<option value="header.jpg">foto1</option>
										<option value="inici.png">foto2</option>
									</select>
								</div>	
								<div class="col-md-2" style="left:13%;top:12px;width: 225px;">
									<button style="height: 31px;color: #FFFFFF;background-color: #337ab7;transition: box-shadow 0.28s cubic-bezier(0.4, 0, 0.2, 1);border-radius: 2px;border-width: 0 !important;overflow: hidden;text-transform: none;    text-align: center; padding: 12px 26px 10px 26px;line-height: 0.25; vertical-align: middle; font-size: 12px;" id="descarga" name="descarga">Descargar Plantilla</button>
								</div>
							</div>	
						</div>
								  <?php 
								  }else{
								  	?>

						<div class="col-md-4">
							<div class="form-group">
								<div class="col-md-4" style="left: 65%;padding-top: 30px;">
								<label>Plantillas</label>
								</div>
								<div class="col-md-2" style="left:68%;top:12px;width: 225px;">
									<select  class="form-control input select2m" data-placeholder="Select..." name="archivo" id="archivo">
										<option value="" selected></option>
										<option value="modelodb.xlsx">modelodb</option>
										<option value="FALSE.xlsx">falso</option>
										<option value="Copia de CamposProveedores (2).xlsx">proveedor</option>
										<option value="header.jpg">foto1</option>
										<option value="inici.png">foto2</option>
									</select>
								</div>	
								<div class="col-md-2" style="left:73%;top:12px;width: 225px;">
									<button style="height: 31px;color: #FFFFFF;background-color: #337ab7;transition: box-shadow 0.28s cubic-bezier(0.4, 0, 0.2, 1);border-radius: 2px;border-width: 0 !important;overflow: hidden;text-transform: none;    text-align: center; padding: 12px 26px 10px 26px;line-height: 0.25; vertical-align: middle; font-size: 12px;" id="descarga" name="descarga">Descargar Plantilla</button>
								</div>
							</div>	
						</div>
								  	<?php
								  }

								  ?>

						<div class="col-md-12">
							<div class="col-md-6">
								<div class="form-group">
									 <div class="col-md-3" style="left: 10%;padding-top: 30px;">
									  	<label>Comentarios Usuario<span style="color:red;">*</span></label>
									</div>

									 <div class="col-md-4 upload-btn-wrapper" style="left:10%;top:12px;width: 450px;">
									<textarea id="comusuario" name="comusuario" style="width: 306px;height: 56px;"></textarea>
									</div>
								</div>

							</div>

							<div class="col-md-6">
								<div class="form-group">
									 <div class="col-md-3" style="left: 10%;padding-top: 30px;">
									  	<label>Comentarios Legal<span style="color:red;">*</span></label>
									</div>

									 <div class="col-md-4 upload-btn-wrapper" style="left:10%;top:12px;width: 450px;">
									<textarea id="comlegal" name="comlegal" style="width: 306px;height: 56px;" readonly="readonly"></textarea>
									</div>
								</div>

							</div>

						</div>

						<div class="row">
							<div class="col-md-offset-5 col-md-8" style="top:55px;">
								<input type="submit" position="center" class="btn btn-success"  name="enviar" id="enviar" value="Enviar"> 	
							</div>
						</div>
					</form>
					<div class="form-actions">
						<div class="row-a">
							<div class="col-md-1" style="display:block;" id="atras5">
								<a href="javascript:;" class="btn blue button-previous" id="atras">
								<i class="m-icon-swapleft m-icon-white"></i></a>
							</div>
							<div class="col-md-offset-1 col-md-9" style="display:none" id="fin2">
								<a href="javascript:;" class="btn yellow button-submit" id="fin">
								Finalizar <i class="m-icon-swapright m-icon-white"></i>  
								</a>
								
							</div>
						</div>
					</div>
					<?php 
				}
				else if($rows['acepcont']=="no"){ 
				?>	
					<form method="POST" id="formtab6" action="fileup.php" enctype="multipart/form-data" target="frame">
						<iframe name="frame" style="display:none"></iframe>
						<h4 class="block" ><b>Contratos</b></h4>
						<div class="col-md-6">
							<div class="form-group">
								
								<?php 
								 if ($ddd['contrato']=="Obligatorio") {		
								 ?>
								 <div class="col-md-3" style="left: 10%;padding-top: 30px;">
								<label>Contrato<span style="color:red;">*</span></label>
								<?php 
								 }else {		
								 ?>
								 <div class="col-md-3" style="left: 12%;padding-top: 30px;">
								<label>Orden de Compra<span style="color:red;">*</span></label>
								<?php 
								 }		
								 ?>
								</div>

								
								  <?php 
								  if ($ddd['contrato']=="Obligatorio") {		
								  ?>
								  <div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: auto;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadob" name="estadob">Sin documento</button>
								  <input type="file" name="contrato1" id="contrato1" required/>
								  <?php 
								  }else {		
								  ?>
								  <div class="col-md-2 upload-btn-wrapper" style="left:11%;top:12px;width: auto;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 62px;" id="estadob" name="estadob">Sin documento</button>
								  <input type="file" name="contrato1" id="contrato1" required/>
								  <?php 
								  }		
								  ?>
								</div>

								<div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: auto;">
								<a href="descargacont.php?archivo=<?php echo $ccc['contra'];?>" style="padding-top: 24px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version anterior</a>
								</div>
								<a class="btn blue" style="left: 86%;margin-top:-11%;" onclick="clausula()">Ver Clausulas</a>

								  <input type="text" name="contra" id="contra" style="display:none;">
							</div>
						</div>

						<?php 
								  if ($ddd['contrato']=="Obligatorio") {		
								  ?>
						<div class="col-md-6">
							<div class="form-group">
								 <div class="col-md-3" style="left: 10%;padding-top: 30px;">
								  	<label>Ficha RUC<span style="color:red;">*</span></label>
								</div>

								  <div class="col-md-10 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadofruc" name="estadofruc">No hay documento cargado</button>
								  <input type="file" name="fruc" id="fruc"/>
								  </div>

								  <div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								<a href="descargacont.php?archivo=<?php echo $ccc['fruc'];?>" style="padding-top:18px;text-transform: none;top:14px;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version anterior</a>
								</div>

								 <input type="text" name="dfruc" id="dfruc" style="display:none;">
							</div>
						</div>
						<div class="col-md-6">
							<div class="form-group">
								 <div class="col-md-3" style="left: 10%;padding-top: 30px;">
								  	<label>DNI de quien firma<span style="color:red;">*</span></label>
								</div>

								 <div class="col-md-10 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadodnif" name="estadodnif">No hay documento cargado</button>
								  <input type="file" name="dnif" id="dnif" />
								</div>

								<div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								<a href="descargacont.php?archivo=<?php echo $ccc['dnif'];?>" style="padding-top:18px;text-transform: none;top:14px;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version anterior</a>
								</div>

								 <input type="text" name="ddnif" id="ddnif" style="display:none;">
							</div>
						</div>
						<div class="col-md-6">
							<div class="form-group">
								 <div class="col-md-3" style="left: 10%;padding-top: 30px;">
								  	<label>Constancia de No Adeudo<span style="color:red;">*</span></label>
								</div>

								 <div class="col-md-10 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadocnadeudo" name="estadocnadeudo">No hay documento cargado</button>
								  <input type="file" name="cnadeudo" id="cnadeudo" />
								</div>

								<div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								<a href="descargacont.php?archivo=<?php echo $ccc['cnadeudo'];?>" style="padding-top:18px;text-transform: none;top:14px;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version anterior</a>
								</div>

								 <input type="text" name="dcnadeudo" id="dcnadeudo" style="display:none;">
								 
							</div>
						</div>
						<div class="col-md-6">
							<div class="form-group">
								 <div class="col-md-3" style="left: 10%;padding-top: 30px;">
								  	<label>Vigencia de Poder<span style="color:red;">*</span></label>
								</div>

								 <div class="col-md-10 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 82px;" id="estadovpoder" name= "estadovpoder">No hay documento cargado</button>
								  <input type="file" name="vpoder" id="vpoder" />
								</div>

								<div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								<a href="descargacont.php?archivo=<?php echo $ccc['vpoder'];?>" style="padding-top:18px;text-transform: none;top:14px;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version anterior</a>
								</div>

								 <input type="text" name="dvpoder" id="dvpoder" style="display:none;">
							</div>

						</div>

						
								  <?php 
								  }		
								  ?>


						<div class="col-md-6">
							<div class="form-group">
								<div class="col-md-3" style="left: 10%;padding-top: 30px;">
								<label>Plantillas</label>
								</div>
								<div class="col-md-4" style="left:80px;padding-top: 30px;">
									<select  class="form-control input select2m" data-placeholder="Select..." name="archivo" id="archivo">
										<option value="" selected></option>
										<option value="modelodb.xlsx">modelodb</option>
										<option value="FALSE.xlsx">falso</option>
										<option value="Copia de CamposProveedores (2).xlsx">proveedor</option>
										<option value="header.jpg">foto1</option>
										<option value="inici.png">foto2</option>
									</select>
								</div>	
								<div class="col-md-4" style="left:80px;padding-top: 30px;">
									<button style="height: 31px;color: #FFFFFF;background-color: #337ab7;transition: box-shadow 0.28s cubic-bezier(0.4, 0, 0.2, 1);border-radius: 2px;border-width: 0 !important;overflow: hidden;text-transform: none;    text-align: center; padding: 12px 26px 10px 26px;line-height: 0.25; vertical-align: middle; font-size: 12px;" id="descarga" name="descarga">Descargar Plantilla</button>
								</div>
							</div>	
						</div>

						<div class="col-md-12">
							<div class="col-md-6">
								<div class="form-group">
									 <div class="col-md-3" style="left: 10%;padding-top: 30px;">
									  	<label>Comentarios Usuario<span style="color:red;">*</span></label>
									</div>

									 <div class="col-md-4 upload-btn-wrapper" style="left:10%;top:12px;width: 450px;">
									<textarea id="comusuario" name="comusuario" style="width: 306px;height: 56px;"><?php echo $ccc['comusuario'];?></textarea>
									</div>
								</div>

							</div>

							<div class="col-md-6">
								<div class="form-group">
									 <div class="col-md-3" style="left: 10%;padding-top: 30px;">
									  	<label>Comentarios Legal<span style="color:red;">*</span></label>
									</div>

									 <div class="col-md-4 upload-btn-wrapper" style="left:10%;top:12px;width: 450px;">
									<textarea id="comlegal" name="comlegal" style="width: 306px;height: 56px;" readonly="readonly"><?php echo $ccc['comlegal'];?></textarea>
									</div>
								</div>

							</div>

						</div>

						<div class="row">
							<div class="col-md-offset-5 col-md-8" style="top:55px;">
								<input type="submit" position="center" class="btn btn-success"  name="enviar" id="enviar" value="Actualizar Contrato"> 	
							</div>
						</div>
					</form>
					<div class="form-actions">
						<div class="row-a">
							<div class="col-md-1" style="display:block;" id="atras5">
								<a href="javascript:;" class="btn blue button-previous" id="atras">
								<i class="m-icon-swapleft m-icon-white"></i></a>
							</div>
							<div class="col-md-offset-1 col-md-9" style="display:none" id="fin2">
								<a href="javascript:;" class="btn yellow button-submit" id="fin">
								Finalizar <i class="m-icon-swapright m-icon-white"></i>  
								</a>
								
							</div>
						</div>
					</div>


				</div>
				<?php 
				}
				else if($rows['acepcont']=="correo"){ 
				?>	
					<form method="POST" id="formtab6" action="fileup.php" enctype="multipart/form-data" target="frame">
						<iframe name="frame" style="display:none"></iframe>
						<h4 class="block" ><b>Contratos</b></h4>
						
						<div class="col-md-4">
							<div class="form-group">
								<div class="col-md-4" style="left: 10%;padding-top: 30px;">
								<?php 
								 if ($ddd['contrato']=="Obligatorio") {		
								 ?>
								<label>Contrato<span style="color:red;">*</span></label>
								<?php 
								 }else {		
								 ?>
								<label>Orden de Compra<span style="color:red;">*</span></label>
								<?php 
								 }		
								 ?>
								</div>

								<div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								<a href="descargacont.php?archivo=<?php echo $ccc['contra'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version actual</a>
								</div>

								<a class="btn blue" style="left: 86%;margin-top:-11%;" onclick="clausula()">Ver Clausulas</a>

								  <input type="text" name="contra" id="contra" style="display:none;">
							</div>
						</div>

						<?php 
							if ($ddd['contrato']=="Obligatorio") {		
						?>
						<div class="col-md-4">
							<div class="form-group">
								 <div class="col-md-4" style="left: 10%;padding-top: 30px;">
								  	<label>Ficha RUC<span style="color:red;">*</span></label>
								</div>
									<div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								<a href="descargacont.php?archivo=<?php echo $ccc['ficharuc'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="fruc" name="fruc"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version actual</a>
								</div>
								 <input type="text" name="dfruc" id="dfruc" style="display:none;">
							</div>
						</div>
						<div class="col-md-4">
							<div class="form-group">
								 <div class="col-md-4" style="left: 10%;padding-top: 30px;">
								  	<label>DNI de quien firma<span style="color:red;">*</span></label>
								</div>

								 <div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								<a href="descargacont.php?archivo=<?php echo $ccc['dnif'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="dnif" name="dnif"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version actual</a>
								</div>
								 <input type="text" name="ddnif" id="ddnif" style="display:none;">
							</div>
						</div>
						<div class="col-md-4">
							<div class="form-group">
								 <div class="col-md-4" style="left: 10%;padding-top: 30px;">
								  	<label>Constancia de No Adeudo<span style="color:red;">*</span></label>
								</div>

								 <div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								<a href="descargacont.php?archivo=<?php echo $ccc['cnadeudo'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cnadeudo" name="cnadeudo"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version actual</a>
								</div>
								 <input type="text" name="dcnadeudo" id="dcnadeudo" style="display:none;">
								 
							</div>
						</div>
						<div class="col-md-4">
							<div class="form-group">
								 <div class="col-md-4" style="left: 10%;padding-top: 30px;">
								  	<label>Vigencia de Poder<span style="color:red;">*</span></label>
								</div>

								 <div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								<a href="descargacont.php?archivo=<?php echo $ccc['vpoder'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="vpoder" name="vpoder"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version actual</a>
								</div>
								 <input type="text" name="dvpoder" id="dvpoder" style="display:none;">
							</div>

						</div>
								  <?php 
								  }

								  ?>

						

						<div class="col-md-12">
							<div class="col-md-6">
								<div class="form-group">
									 <div class="col-md-3" style="left: 10%;padding-top: 30px;">
									  	<label>Comentarios Usuario<span style="color:red;">*</span></label>
									</div>

									 <div class="col-md-4 upload-btn-wrapper" style="left:10%;top:12px;width: 450px;">
									<textarea id="comusuario" name="comusuario" style="width: 306px;height: 56px;" readonly="readonly"><?php echo $ccc['comusuario'];?></textarea>
									</div>
								</div>

							</div>

							<div class="col-md-6">
								<div class="form-group">
									 <div class="col-md-3" style="left: 10%;padding-top: 30px;">
									  	<label>Comentarios Legal<span style="color:red;">*</span></label>
									</div>

									 <div class="col-md-4 upload-btn-wrapper" style="left:10%;top:12px;width: 450px;">
									<textarea id="comlegal" name="comlegal" style="width: 306px;height: 56px;" readonly="readonly"><?php echo $ccc['comlegal'];?></textarea>
									</div>
								</div>

							</div>

						</div>
						<div class="row">
							<div class="col-md-offset-5 col-md-8" style="top:55px;">
								<input type="button" position="center" class="btn btn-default"  name="enviar" id="enviar" value="Documentos en evaluación" disabled> 	
							</div>
						</div>

					</form>
					<div class="form-actions">
						<div class="row-a">
							<div class="col-md-1" style="display:block;" id="atras5">
								<a href="javascript:;" class="btn blue button-previous" id="atras">
								<i class="m-icon-swapleft m-icon-white"></i></a>
							</div>
							<div class="col-md-offset-1 col-md-9" style="display:none" id="fin2">
								<a href="javascript:;" class="btn yellow button-submit" id="fin">
								Finalizar <i class="m-icon-swapright m-icon-white"></i>  
								</a>
								
							</div>
						</div>
					</div>
					<?php 
				}
				else if($rows['acepcont']=="si"){ 
				?>	
					<h4 class="block" ><b>Contratos</b></h4>
						<div class="col-md-4">
							<div class="form-group">
								
								<?php 
								 if ($ddd['contrato']=="Obligatorio") {		
								 ?>
								 <div class="col-md-4" style="left: 10%;padding-top: 30px;">
								<label>Contrato<span style="color:red;">*</span></label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								<a href="descargacont.php?archivo=<?php echo $ccc['contra'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version Final</a>
								</div>
								<a class="btn blue" style="left: 86%;margin-top:-11%;" onclick="clausula()">Ver Clausulas</a>
								<?php 
								 }else {		
								 ?>
								 <div class="col-md-4" style="left: 18%;padding-top: 30px;">
								<label>Orden de Compra<span style="color:red;">*</span></label>
								</div>
								<div class="col-md-2 upload-btn-wrapper" style="left:21%;top:12px;width: 225px;">
								<a href="descargacont.php?archivo=<?php echo $ccc['contra'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version Final</a>
								</div>
								<?php 
								 }		
								 ?>
											
								  <input type="text" name="contra" id="contra" style="display:none;">
							</div>
						</div>

						<?php 
							if ($ddd['contrato']=="Obligatorio") {		
						?>
						<div class="col-md-4">
							<div class="form-group">
								 <div class="col-md-4" style="left: 10%;padding-top: 30px;">
								  	<label>Ficha RUC<span style="color:red;">*</span></label>
								</div>
									<div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								<a href="descargacont.php?archivo=<?php echo $ccc['ficharuc'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="fruc" name="fruc"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version actual</a>
								</div>
								 <input type="text" name="dfruc" id="dfruc" style="display:none;">
							</div>
						</div>
						<div class="col-md-4">
							<div class="form-group">
								 <div class="col-md-4" style="left: 10%;padding-top: 30px;">
								  	<label>DNI de quien firma<span style="color:red;">*</span></label>
								</div>

								 <div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								<a href="descargacont.php?archivo=<?php echo $ccc['dnif'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="dnif" name="dnif"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version actual</a>
								</div>
								 <input type="text" name="ddnif" id="ddnif" style="display:none;">
							</div>
						</div>
						<div class="col-md-4">
							<div class="form-group">
								 <div class="col-md-4" style="left: 10%;padding-top: 30px;">
								  	<label>Constancia de No Adeudo<span style="color:red;">*</span></label>
								</div>

								 <div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								<a href="descargacont.php?archivo=<?php echo $ccc['cnadeudo'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cnadeudo" name="cnadeudo"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version actual</a>
								</div>
								 <input type="text" name="dcnadeudo" id="dcnadeudo" style="display:none;">
								 
							</div>
						</div>
						<div class="col-md-4">
							<div class="form-group">
								 <div class="col-md-4" style="left: 10%;padding-top: 30px;">
								  	<label>Vigencia de Poder<span style="color:red;">*</span></label>
								</div>

								 <div class="col-md-2 upload-btn-wrapper" style="left:10%;top:12px;width: 225px;">
								<a href="descargacont.php?archivo=<?php echo $ccc['vpoder'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="vpoder" name="vpoder"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version actual</a>
								</div>
								 <input type="text" name="dvpoder" id="dvpoder" style="display:none;">
							</div>

						</div>
								  <?php 
								  }

								  ?>

						<div class="col-md-12">
							<div class="col-md-6">
								<div class="form-group">
									 <div class="col-md-3" style="left: 5%;padding-top: 30px;">
									  	<label>Comentarios Usuario<span style="color:red;">*</span></label>
									</div>

									 <div class="col-md-4 upload-btn-wrapper" style="left:3%;top:12px;width: 450px;">
									<textarea id="comusuario" name="comusuario" style="width: 306px;height: 56px;"readonly="readonly"><?php echo $ccc['comusuario'];?></textarea>
									</div>
								</div>

							</div>

							<div class="col-md-6">
								<div class="form-group">
									 <div class="col-md-3" style="left: 26%;padding-top: 30px;">
									  	<label>Comentarios Legal<span style="color:red;">*</span></label>
									</div>

									 <div class="col-md-4 upload-btn-wrapper" style="left:24%;top:12px;width: 450px;">
									<textarea id="comlegal" name="comlegal" style="width: 306px;height: 56px;"readonly="readonly"><?php echo $ccc['comlegal'];?></textarea>
									</div>
								</div>

							</div>

						</div>
						<div class="row">
							<div class="col-md-offset-5 col-md-8">
								<div style="margin-top:20px;"> 
								 <a class="btn gray col-md-offset-1" style="left:3%;" href="resumen.php?id=<?php echo $_SESSION['id'];?>">
								 Ver Resumen</a>
								</div> 	
							</div>
						</div>
						<div class="col-md-12"><hr style="border-top-width: 1px;border-top-style: solid;border-top-color: #aaa;"></div>
						<?php 
						while($firm = mysqli_fetch_array($resfirmado,MYSQLI_ASSOC))
						{
							if ($firm['extra3']=="") {
								?>
						<form method="POST" id="formtab7" action="contratofirmado.php" enctype="multipart/form-data" target="framex">
						<iframe name="framex" style="display:none"></iframe>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-2" style="left: 4%;padding-top: 30px;">
								  	<label>Contrato Firmado<span style="color:red;">*</span></label>
								</div>

								<div class="col-md-2 upload-btn-wrapper" style="left:-2%;top:12px;width: auto;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 62px;" id="estadof" name="estadof">Sin documento</button>
								  <input type="file" name="contratofirmado" id="contratofirmado" required/>
								</div>
								  <input type="text" name="dcontratofirmado" id="dcontratofirmado" style="display:none;">
							</div>
							<div class="col-md-3" style="left:42%;"><input type="text" name="resultadosestado" id ="resultadosestado" value="Se completaron 0 de 15 campos" readonly="" style="width: 204px;border:none;"></div>
						</div>
						<div class="col-md-12" style="overflow: scroll;">
							<br>
							<table class="table table-bordered dataTables_wrapper no-footer" style="margin: 0 auto;width: 100%;font-size:12px;">
								<tr>
									<th style="vertical-align: middle; text-align:center;">Contraparte</th>
									<th style="vertical-align: middle; text-align:center;">Objeto</th>
									<th style="vertical-align: middle; text-align:center;">Fecha de Suscripción</th>
									<th style="vertical-align: middle; text-align:center;">Fecha de Inicio</th>
									<th style="vertical-align: middle; text-align:center;">Fecha de Vencimiento</th>
									<th style="vertical-align: middle; text-align:center;">Renovación Automática</th>
									<th style="vertical-align: middle; text-align:center;">Observaciones</th>
									<th style="vertical-align: middle; text-align:center;">Resolución Anticipada</th>
									<th style="vertical-align: middle; text-align:center;">Penalidad</th>
									<th style="vertical-align: middle; text-align:center;">Cláusula de Confidencialidad</th>
									<th style="vertical-align: middle; text-align:center;">Cláusula de Riesgo Operativo</th>
									<th style="vertical-align: middle; text-align:center;">Cláusula Acuerdo Niveles de Servicio</th>
									<th style="vertical-align: middle; text-align:center;">Garantía por incumplimiento en el Servicio</th>
									<th style="vertical-align: middle; text-align:center;">Solución de conflictos</th>
									<th style="vertical-align: middle; text-align:center;">Grente Responsable</th>
								</tr>
								<tr>
									<td><input type="text" name="legal1" id="legal1" class="legal" style=" height: 40px;" onclick="getelegido();" readonly=""></td>
									<td><input type="text" name="legal2" id="legal2" class="legal" style=" height: 40px;"></td>
									<td><input type="date" name="legal3" id="legal3" class="legal" style="text-align:center;"></td>
									<td><input type="date" name="legal4" id="legal4" class="legal" style="text-align:center;"></td>
									<td><input type="date" name="legal5" id="legal5" class="legal" style="text-align:center;"></td>
									<td>
										<!-- <input type="text" name="legal6" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal6" id="legal6"> 
											<option value="" selected></option>
											<option value="si" >Si</option>
											<option value="no" >No</option>
										</select>
									</td>
									<td><input type="text" name="legal7" id="legal7" class="legal" style=" height: 40px;"></td>
									<td><input type="text" name="legal8" id="legal8" class="legal" style=" height: 40px;"></td>
									<td><input type="text" name="legal9" id="legal9" class="legal" style=" height: 40px;"></td>
									<td>
										<!-- <input type="text" name="legal10" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal10" id="legal10"> 
											<option value="" selected></option>
											<option value="si" >Si</option>
											<option value="no" >No</option>
										</select>
									</td>
									<td>
										<!-- <input type="text" name="legal11" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal11" id="legal11"> 
											<option value="" selected></option>
											<option value="si" >Si</option>
											<option value="no" >No</option>
										</select>
									</td>
									<td>
										<!-- <input type="text" name="legal12" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal12" id="legal12"> 
											<option value="" selected></option>
											<option value="si" >Si</option>
											<option value="no" >No</option>
										</select>
									</td>
									<td>
										<!-- <input type="text" name="legal13" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal13" id="legal13"> 
											<option value="" selected></option>
											<option value="si" >Si</option>
											<option value="no" >No</option>
										</select>
									</td>
									<td>
										<!-- <input type="text" name="legal14" id="legal14" class="legal" style=" height: 40px;">-->
										<div class="solucionc">
										<select class="form-control input-large select2m bg-gray-steel legal" data-placeholder="Select..." name="legal14" id="legal14"> 
											<option value="no hay nada" selected>no hay nada</option>
										</select>
										</div>
									</td>
									<td><input type="text" name="legal15" id="legal15" class="legal" style=" height: 40px;"></td>
								</tr>
							</table>
						</div>
						<div class="col-md-12"><br><button type="submit" class="btn green" style="left:47%;">Registrar</button><br></div>
					</form>	

					<div class="form-actions">
						<div class="row-a">
							<div class="col-md-1" style="display:block;" id="atras5">
								<a href="javascript:;" class="btn blue button-previous" id="atras">
								<i class="m-icon-swapleft m-icon-white"></i></a>
							</div>
							<div class="col-md-offset-1 col-md-9" style="display:none" id="fin2">
								<a href="javascript:;" class="btn yellow button-submit" id="fin">
								Finalizar <i class="m-icon-swapright m-icon-white"></i>  
								</a>
								
							</div>
						</div>
					</div>
							<?php

							}elseif ($firm['extra3']=="si") {
							?>

							<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-2" style="left: 4%;padding-top: 30px;">
								  	<label>Contrato Firmado<span style="color:red;">*</span></label>
								</div>

								<div class="col-md-2 upload-btn-wrapper" style="left:-2%;top:12px;width: auto;">
								  <a href="descargacont.php?archivo=<?php echo $firm['extra1'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version Final</a>
								</div>
							</div>
							<div class="col-md-3" style="left:42%;"><input type="text" name="resultadosestado" id ="resultadosestado" value="Se completaron 15 de 15 campos" readonly="" style="width: 204px;border:none;"></div>
						</div>
						<div class="col-md-12" style="overflow: scroll;">
							<br>
							<table class="table table-bordered dataTables_wrapper no-footer" style="margin: 0 auto;width: 100%;font-size:12px;">
								<tr>
									<th style="vertical-align: middle; text-align:center;">Contraparte</th>
									<th style="vertical-align: middle; text-align:center;">Objeto</th>
									<th style="vertical-align: middle; text-align:center;">Fecha de Suscripción</th>
									<th style="vertical-align: middle; text-align:center;">Fecha de Inicio</th>
									<th style="vertical-align: middle; text-align:center;">Fecha de Vencimiento</th>
									<th style="vertical-align: middle; text-align:center;">Renovación Automática</th>
									<th style="vertical-align: middle; text-align:center;">Observaciones</th>
									<th style="vertical-align: middle; text-align:center;">Resolución Anticipada</th>
									<th style="vertical-align: middle; text-align:center;">Penalidad</th>
									<th style="vertical-align: middle; text-align:center;">Cláusula de Confidencialidad</th>
									<th style="vertical-align: middle; text-align:center;">Cláusula de Riesgo Operativo</th>
									<th style="vertical-align: middle; text-align:center;">Cláusula Acuerdo Niveles de Servicio</th>
									<th style="vertical-align: middle; text-align:center;">Garantía por incumplimiento en el Servicio</th>
									<th style="vertical-align: middle; text-align:center;">Solución de conflictos</th>
									<th style="vertical-align: middle; text-align:center;">Grente Responsable</th>
								</tr>
								<tr>
									<td><input type="text" name="legal1" id="legal1" class="legal" style=" height: 40px;" disabled="" value="<?php echo $firm['contraparte'] ;?>"></td>
									<td><input type="text" name="legal2" id="legal2" class="legal" style=" height: 40px;" disabled="" value="<?php echo $firm['objeto'] ;?>" ></td>
									<td><input type="date" name="legal3" id="legal3" class="legal" style="text-align:center;" disabled="" value="<?php echo $firm['fecha_suscripcion'] ;?>" ></td>
									<td><input type="date" name="legal4" id="legal4" class="legal" style="text-align:center;" disabled="" value="<?php echo $firm['fecha_inicio'] ;?>" ></td>
									<td><input type="date" name="legal5" id="legal5" class="legal" style="text-align:center;" disabled="" value="<?php echo $firm['fecha_vencimiento'] ;?>" ></td>
									<td>
										<!-- <input type="text" name="legal6" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal6" id="legal6" disabled=""> 
											<option value="<?php echo $firm['renov_automatica'] ;?>" selected><?php echo $firm['renov_automatica'] ;?></option>
										</select>
									</td>
									<td><input type="text" name="legal7" id="legal7" class="legal" style=" height: 40px;" disabled="" value="<?php echo $firm['observacion'] ;?>"></td>
									<td><input type="text" name="legal8" id="legal8" class="legal" style=" height: 40px;" disabled="" value="<?php echo $firm['resol_anticipada'] ;?>"></td>
									<td><input type="text" name="legal9" id="legal9" class="legal" style=" height: 40px;" disabled="" value="<?php echo $firm['penalidad'] ;?>"></td>
									<td>
										<!-- <input type="text" name="legal10" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal10" id="legal10" disabled=""> 
											<option value="<?php echo $firm['clau_confidencial'] ;?>" selected><?php echo $firm['clau_confidencial'] ;?></option>
										</select>
									</td>
									<td>
										<!-- <input type="text" name="legal11" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal11" id="legal11" disabled=""> 
											<option value="<?php echo $firm['extra2'] ;?>" selected><?php echo $firm['extra2'] ;?></option>
											<option value="si" >Si</option>
											<option value="no" >No</option>
										</select>
									</td>
									<td>
										<!-- <input type="text" name="legal12" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal12" id="legal12" disabled=""> 
											<option value="<?php echo $firm['clau_acuerdo'] ;?>" selected><?php echo $firm['clau_acuerdo'] ;?></option>
											<option value="si" >Si</option>
											<option value="no" >No</option>
										</select>
									</td>
									<td>
										<!-- <input type="text" name="legal13" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal13" id="legal13" disabled=""> 
											<option value="<?php echo $firm['garantia_incum'] ;?>" selected><?php echo $firm['garantia_incum'] ;?></option>
											<option value="si" >Si</option>
											<option value="no" >No</option>
										</select>
									</td>
									<td>
										<!-- <input type="text" name="legal14" id="legal14" class="legal" style=" height: 40px;">-->
										<div class="">
										<select class="form-control input-large select2m bg-gray-steel legal" data-placeholder="Select..." name="legal14" id="legal14" disabled=""> 
											<option value="<?php echo $_SESSION['solucion'] ;?>" selected><?php echo $_SESSION['solucion'] ;?></option>
										</select>
										</div>
									</td>
									<td><input type="text" name="legal15" id="legal15" class="legal" style=" height: 40px;" disabled="" value="<?php echo $firm['gerente_resp'] ;?>"></td>
								</tr>
							</table>
						</div>
						
						<div class="form-actions">
						<div class="row-a">
							<div class="col-md-1" style="display:block;margin-top:2%;" id="atras5">
								<a href="javascript:;" class="btn blue button-previous" id="atras">
								<i class="m-icon-swapleft m-icon-white"></i></a>
							</div>
							<div class="col-md-offset-1 col-md-9" style="display:none" id="fin2">
								<a href="javascript:;" class="btn yellow button-submit" id="fin">
								Finalizar <i class="m-icon-swapright m-icon-white"></i>  
								</a>
								
							</div>
						</div>
					</div>
							<?php	
							}elseif ($firm['extra3']=="no") {
								
						?>
						
						<form method="POST" id="formtab7" action="contratofirmado.php" enctype="multipart/form-data" target="framex">
						<iframe name="framex" style="display:none"></iframe>
						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-2" style="left: 4%;padding-top: 30px;">
								  	<label>Contrato Firmado<span style="color:red;">*</span></label>
								</div>

								<div class="col-md-2 upload-btn-wrapper" style="left:-2%;top:12px;width: auto;">
								  <button class="btn btn-lg grey-cascade" style="text-transform: none;font-size: 12px;height: 62px;" id="estadof" name="estadof">Nuevo documento</button>
								  <input type="file" name="contratofirmado" id="contratofirmado" required/>
								</div>

								<div class="col-md-2 upload-btn-wrapper" style="left:0%;top:12px;width: 225px;">
								<a href="descargacont.php?archivo=<?php echo $firm['extra1'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version Anterior</a>
								</div>

								  <input type="text" name="dcontratofirmado" id="dcontratofirmado" style="display:none;">
							</div>
							<div class="col-md-3" style="left:42%;"><input type="text" name="resultadosestado" id ="resultadosestado" value="Se completaron 15 de 15 campos" readonly="" style="width: 204px;border:none;"></div>
						</div>
						<div class="col-md-12" style="overflow: scroll;">
							<br>
							<table class="table table-bordered dataTables_wrapper no-footer" style="margin: 0 auto;width: 100%;font-size:12px;">
								<tr>
									<th style="vertical-align: middle; text-align:center;">Contraparte</th>
									<th style="vertical-align: middle; text-align:center;">Objeto</th>
									<th style="vertical-align: middle; text-align:center;">Fecha de Suscripción</th>
									<th style="vertical-align: middle; text-align:center;">Fecha de Inicio</th>
									<th style="vertical-align: middle; text-align:center;">Fecha de Vencimiento</th>
									<th style="vertical-align: middle; text-align:center;">Renovación Automática</th>
									<th style="vertical-align: middle; text-align:center;">Observaciones</th>
									<th style="vertical-align: middle; text-align:center;">Resolución Anticipada</th>
									<th style="vertical-align: middle; text-align:center;">Penalidad</th>
									<th style="vertical-align: middle; text-align:center;">Cláusula de Confidencialidad</th>
									<th style="vertical-align: middle; text-align:center;">Cláusula de Riesgo Operativo</th>
									<th style="vertical-align: middle; text-align:center;">Cláusula Acuerdo Niveles de Servicio</th>
									<th style="vertical-align: middle; text-align:center;">Garantía por incumplimiento en el Servicio</th>
									<th style="vertical-align: middle; text-align:center;">Solución de conflictos</th>
									<th style="vertical-align: middle; text-align:center;">Grente Responsable</th>
								</tr>
								<tr>
									<td><input type="text" name="legal1" id="legal1" class="legal" style=" height: 40px;" disabled="" value="<?php echo $firm['contraparte'] ;?>"></td>
									<td><input type="text" name="legal2" id="legal2" class="legal" style=" height: 40px;"  value="<?php echo $firm['objeto'] ;?>" ></td>
									<td><input type="date" name="legal3" id="legal3" class="legal" style="text-align:center;"  value="<?php echo $firm['fecha_suscripcion'] ;?>" ></td>
									<td><input type="date" name="legal4" id="legal4" class="legal" style="text-align:center;"  value="<?php echo $firm['fecha_inicio'] ;?>" ></td>
									<td><input type="date" name="legal5" id="legal5" class="legal" style="text-align:center;"  value="<?php echo $firm['fecha_vencimiento'] ;?>" ></td>
									<td>
										<!-- <input type="text" name="legal6" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal6" id="legal6"> 
											<option value="<?php echo $firm['renov_automatica'] ;?>" selected><?php echo $firm['renov_automatica'] ;?></option>
										</select>
									</td>
									<td><input type="text" name="legal7" id="legal7" class="legal" style=" height: 40px;"  value="<?php echo $firm['observacion'] ;?>"></td>
									<td><input type="text" name="legal8" id="legal8" class="legal" style=" height: 40px;"  value="<?php echo $firm['resol_anticipada'] ;?>"></td>
									<td><input type="text" name="legal9" id="legal9" class="legal" style=" height: 40px;"  value="<?php echo $firm['penalidad'] ;?>"></td>
									<td>
										<!-- <input type="text" name="legal10" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal10" id="legal10"> 
											<option value="<?php echo $firm['clau_confidencial'] ;?>" selected><?php echo $firm['clau_confidencial'] ;?></option>
										</select>
									</td>
									<td>
										<!-- <input type="text" name="legal11" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal11" id="legal11"> 
											<option value="<?php echo $firm['extra2'] ;?>" selected><?php echo $firm['extra2'] ;?></option>
											<option value="si" >Si</option>
											<option value="no" >No</option>
										</select>
									</td>
									<td>
										<!-- <input type="text" name="legal12" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal12" id="legal12"> 
											<option value="<?php echo $firm['clau_acuerdo'] ;?>" selected><?php echo $firm['clau_acuerdo'] ;?></option>
											<option value="si" >Si</option>
											<option value="no" >No</option>
										</select>
									</td>
									<td>
										<!-- <input type="text" name="legal13" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal13" id="legal13"> 
											<option value="<?php echo $firm['garantia_incum'] ;?>" selected><?php echo $firm['garantia_incum'] ;?></option>
											<option value="si" >Si</option>
											<option value="no" >No</option>
										</select>
									</td>
									<td>
										<!-- <input type="text" name="legal14" id="legal14" class="legal" style=" height: 40px;">-->
										<div class="solucionc">
										<select class="form-control input-large select2m bg-gray-steel legal" data-placeholder="Select..." name="legal14" id="legal14">
											<option value="<?php echo $_SESSION['solucion'] ;?>" selected><?php echo $_SESSION['solucion'] ;?></option>
										</select>
										</div>
									</td>
									<td><input type="text" name="legal15" id="legal15" class="legal" style=" height: 40px;"  value="<?php echo $firm['gerente_resp'] ;?>"></td>
								</tr>
							</table>
						</div>
						<div class="col-md-12"><br><button type="submit" class="btn green" style="left:47%;">Registrar</button><br></div>
					</form>	

					<div class="form-actions">
						<div class="row-a">
							<div class="col-md-1" style="display:block;" id="atras5">
								<a href="javascript:;" class="btn blue button-previous" id="atras">
								<i class="m-icon-swapleft m-icon-white"></i></a>
							</div>
							<div class="col-md-offset-1 col-md-9" style="display:none" id="fin2">
								<a href="javascript:;" class="btn yellow button-submit" id="fin">
								Finalizar <i class="m-icon-swapright m-icon-white"></i>  
								</a>
								
							</div>
						</div>
					</div>
						<?php		

							}elseif ($firm['extra3']=="sa") {
								
						?>

						<div class="col-md-12">
							<div class="form-group">
								<div class="col-md-2" style="left: 4%;padding-top: 30px;">
								  	<label>Contrato Firmado<span style="color:red;">*</span></label>
								</div>

								<div class="col-md-2 upload-btn-wrapper" style="left:-2%;top:12px;width: auto;">
								  <a href="descargacont.php?archivo=<?php echo $firm['extra1'];?>" style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn blue fileinput-button"  type="button" id="cot" name="cot"><i class="fa fa-cloud-download" id="control" name="control"></i> Descargar version Actual</a>
								</div>

								<div class="col-md-2 upload-btn-wrapper" style="left:3%;top:12px;width: auto;">
								<a style="padding-top:22px;text-transform: none;font-size: 12px;height: 60px;" class="btn yellow fileinput-button"  type="button" id="cot" name="cot">El contrato y la información ingresada esta siendo revisada por el Área Legal</a>
								</div>

							</div>
							<div class="col-md-3" style="left:42%;"><input type="text" name="resultadosestado" id ="resultadosestado" value="Se completaron 15 de 15 campos" readonly="" style="width: 204px;border:none;"></div>
						</div>
						<div class="col-md-12" style="overflow: scroll;">
							<br>
							<table class="table table-bordered dataTables_wrapper no-footer" style="margin: 0 auto;width: 100%;font-size:12px;">
								<tr>
									<th style="vertical-align: middle; text-align:center;">Contraparte</th>
									<th style="vertical-align: middle; text-align:center;">Objeto</th>
									<th style="vertical-align: middle; text-align:center;">Fecha de Suscripción</th>
									<th style="vertical-align: middle; text-align:center;">Fecha de Inicio</th>
									<th style="vertical-align: middle; text-align:center;">Fecha de Vencimiento</th>
									<th style="vertical-align: middle; text-align:center;">Renovación Automática</th>
									<th style="vertical-align: middle; text-align:center;">Observaciones</th>
									<th style="vertical-align: middle; text-align:center;">Resolución Anticipada</th>
									<th style="vertical-align: middle; text-align:center;">Penalidad</th>
									<th style="vertical-align: middle; text-align:center;">Cláusula de Confidencialidad</th>
									<th style="vertical-align: middle; text-align:center;">Cláusula de Riesgo Operativo</th>
									<th style="vertical-align: middle; text-align:center;">Cláusula Acuerdo Niveles de Servicio</th>
									<th style="vertical-align: middle; text-align:center;">Garantía por incumplimiento en el Servicio</th>
									<th style="vertical-align: middle; text-align:center;">Solución de conflictos</th>
									<th style="vertical-align: middle; text-align:center;">Grente Responsable</th>
								</tr>
								<tr>
									<td><input type="text" name="legal1" id="legal1" class="legal" style=" height: 40px;" disabled="" value="<?php echo $firm['contraparte'] ;?>"></td>
									<td><input type="text" name="legal2" id="legal2" class="legal" style=" height: 40px;" disabled="" value="<?php echo $firm['objeto'] ;?>" ></td>
									<td><input type="date" name="legal3" id="legal3" class="legal" style="text-align:center;" disabled="" value="<?php echo $firm['fecha_suscripcion'] ;?>" ></td>
									<td><input type="date" name="legal4" id="legal4" class="legal" style="text-align:center;" disabled="" value="<?php echo $firm['fecha_inicio'] ;?>" ></td>
									<td><input type="date" name="legal5" id="legal5" class="legal" style="text-align:center;" disabled="" value="<?php echo $firm['fecha_vencimiento'] ;?>" ></td>
									<td>
										<!-- <input type="text" name="legal6" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal6" id="legal6" disabled=""> 
											<option value="<?php echo $firm['renov_automatica'] ;?>" selected><?php echo $firm['renov_automatica'] ;?></option>
										</select>
									</td>
									<td><input type="text" name="legal7" id="legal7" class="legal" style=" height: 40px;" disabled="" value="<?php echo $firm['observacion'] ;?>"></td>
									<td><input type="text" name="legal8" id="legal8" class="legal" style=" height: 40px;" disabled="" value="<?php echo $firm['resol_anticipada'] ;?>"></td>
									<td><input type="text" name="legal9" id="legal9" class="legal" style=" height: 40px;" disabled="" value="<?php echo $firm['penalidad'] ;?>"></td>
									<td>
										<!-- <input type="text" name="legal10" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal10" id="legal10" disabled=""> 
											<option value="<?php echo $firm['clau_confidencial'] ;?>" selected><?php echo $firm['clau_confidencial'] ;?></option>
										</select>
									</td>
									<td>
										<!-- <input type="text" name="legal11" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal11" id="legal11" disabled=""> 
											<option value="<?php echo $firm['extra2'] ;?>" selected><?php echo $firm['extra2'] ;?></option>
											<option value="si" >Si</option>
											<option value="no" >No</option>
										</select>
									</td>
									<td>
										<!-- <input type="text" name="legal12" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal12" id="legal12" disabled=""> 
											<option value="<?php echo $firm['clau_acuerdo'] ;?>" selected><?php echo $firm['clau_acuerdo'] ;?></option>
											<option value="si" >Si</option>
											<option value="no" >No</option>
										</select>
									</td>
									<td>
										<!-- <input type="text" name="legal13" class="legal" style=" height: 40px;"> -->
										<select class="form-control input-xsmall select2m bg-gray-steel legal" data-placeholder="Select..." name="legal13" id="legal13" disabled=""> 
											<option value="<?php echo $firm['garantia_incum'] ;?>" selected><?php echo $firm['garantia_incum'] ;?></option>
											<option value="si" >Si</option>
											<option value="no" >No</option>
										</select>
									</td>
									<td>
										<!-- <input type="text" name="legal14" id="legal14" class="legal" style=" height: 40px;">-->
										<div class="solucionc">
										<select class="form-control input-large select2m bg-gray-steel legal" data-placeholder="Select..." name="legal14" id="legal14" disabled="">
											<option value="<?php echo $_SESSION['solucion'] ;?>" selected><?php echo $_SESSION['solucion'] ;?></option>
										</select>
										</div>
									</td>
									<td><input type="text" name="legal15" id="legal15" class="legal" style=" height: 40px;" disabled="" value="<?php echo $firm['gerente_resp'] ;?>"></td>
								</tr>
							</table>
						</div>
						

						<div class="form-actions">
						<div class="row-a">
							<div class="col-md-1" style="display:block;margin-top:2%;" id="atras5">
								<a href="javascript:;" class="btn blue button-previous" id="atras">
								<i class="m-icon-swapleft m-icon-white"></i></a>
							</div>
							<div class="col-md-offset-1 col-md-9" style="display:none" id="fin2">
								<a href="javascript:;" class="btn yellow button-submit" id="fin">
								Finalizar <i class="m-icon-swapright m-icon-white"></i>  
								</a>
								
							</div>
						</div>
					</div>
						<?php		
							}
						}
						?>
						
					
					
					<?php 
				}
			}
				?>

			</div>
		</div>
		</div>
		</div>
		</div>
		</div>
	</div>
</div>
<div id="tipo_proveedor" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="380">
	<div class="modal-header">
		<button type="button" class="close" data-dismiss="modal" aria-hidden="true" id="ceirratipo" name="ceirratipo"></button>
		<h4 class="modal-title"><b>Consideraciones del Proveedor</b></h4>
  	</div>
			<div class="modal-body" id ="contenido_tipo_proveedor">
					
			</div>
</div>
<div id="tipo_clausula" class="modal fade" tabindex="-1" data-backdrop="static" data-keyboard="false" data-width="400px" style="width:400px;">
	<div class="modal-header">
		<button type="button" class="close" data-dismiss="modal" aria-hidden="true"></button>
		<h4 class="modal-title"><b>Listado de Cláusulas Necesarias dentro del Contrato</b></h4>
  	</div>
			<div class="modal-body" id ="contenido_clausula">
					
			</div>
</div>

<script src="assets/global/plugins/bootstrap-toastr/toastr.js"></script>
<script src="assets/admin/pages/scripts/ui-toastr.js"></script>

<!-- <script type="text/javascript" src="http://code.jquery.com/jquery-3.2.1.min.js"></script> -->
<script type="text/javascript" src="js/jquery-3.2.1.min.js"></script>
<script src="assets/global/plugins/bootstrap-modal/js/bootstrap-modalmanager.js" type="text/javascript"></script>
<script src="assets/global/plugins/bootstrap-modal/js/bootstrap-modal.js" type="text/javascript"></script>
<!-- <link rel="canonical" href="https://craftpip.github.io/jquery-confirm"/> -->
<link rel="stylesheet" type="text/css" href="css/jquery-confirm.css"/>
<script type="text/javascript" src="js/jquery-confirm.js"></script>

<script type="text/javascript">
function comprobar(){

var econ = $("#peconomico").val();  
var t = $("#ptecnico").val();
if(econ > 99 || econ < 40){
	$.alert({
          title: 'Alerta',
          content: 'El valor ingresado no puede ser mayor a 99 o menor a 40, por favor corregir!',
          
          icon: 'fa fa-close',
          type: 'blue',
          buttons: {
              confirm: {
                  text: 'OK',
                  btnClass: 'btn-blue',
              }
          }
      });
 document.getElementById('peconomico').value= 40;
}
if (t > 0) {
	var suma = parseInt(t) + parseInt(econ);
	if( suma != 100){
	$('#anuncio').val("La suma de porcentajes debe ser 100, por favor corregir");
	$('#anuncio').attr("style","border:none;text-align:center;font-size:12px;color:red;font-weight: bold");
	}else{
	$('#anuncio').val("La suma de porcentajes es 100");
	$('#anuncio').attr("style","border:none;text-align:center;font-size:12px;color:green;font-weight: bold");
	}
}

}

function comprobar2(){

var tec = $("#ptecnico").val();  
var e = $("#peconomico").val();

var suma = parseInt(tec) + parseInt(e);

if( suma != 100){
$('#anuncio').val("La suma de porcentajes debe ser 100, por favor corregir");
$('#anuncio').attr("style","border:none;text-align:center;font-size:12px;color:red;font-weight: bold");
}else{
	$('#anuncio').val("La suma de porcentajes es 100");
	$('#anuncio').attr("style","border:none;text-align:center;font-size:12px;color:green;font-weight: bold");
	}

}


</script>
<!-- <script src="http://nosir.github.io/cleave.js/dist/cleave.min.js"></script>

<script type="text/javascript">
	var cleave = new Cleave('.gsto', {
    numeral: true,
    numeralThousandsGroupStyle: 'thousand'
});
	$('.gsto').on('input',function(){
		var texto = $('#gastop').val();
		$('#gasto').attr("value",texto.replace(/,/g,''));
		console.log($('#gastop').val());
		console.log($('#gasto').val());
	});
</script> -->
<script type="text/javascript">
		function tipop(){
		$.ajax({
			   url:"tipo_proveedor.php",
			   method:"POST",
			   success:function(data){
			    $('#contenido_tipo_proveedor').html(data);
			    $('#tipo_proveedor').modal('show');
			   }
			   });
	}

		function clausula(){
		$.ajax({
			   url:"clausulas.php",
			   method:"POST",
			   success:function(data){
			    $('#contenido_clausula').html(data);
			    $('#tipo_clausula').modal('show');
			   }
			   });
	}
		function getelegido(){
		$.ajax({
			   url:"elegidoproveedor.php",
			   method:"POST",
			   success:function(data){
			   	console.log(data);
			    $('#legal1').val(data);
			   }
			   });
	}

function resultado(){
	$("#errorsubida").attr("style", "display:none");
	$("#subido").attr("style", "display:none");
	$("#info").attr("style", "display:block");
}	
function resultadoOk(){
	$("#info").attr("style", "display:none");
	$("#errorsubida").attr("style", "display:none");
	$("#subido").attr("style", "display:block");
    $("#subido").html('Los archivos han sido subidos exitosamente.');
} 
function resultadoErroneo(){
	$("#info").attr("style", "display:none");
	$("#subido").attr("style", "display:none");
	$("#errorsubida").attr("style", "display:block");
    $("#errorsubida").html('Ha surgido un error y no se ha podido subir el archivo.');
}

function borra(){
	$("#errorsubida").attr("style", "display:none");
	console.log("luego de borrar" + $("#errorsubida").attr("style"));
}

$(document).ready(function(){
    completar();
});
</script>

<script type="text/javascript">
	$('#descarga').on('click', function(e){  
		var dsc = $('#archivo').val();
		if (dsc == "") {
			$.alert({
          title: 'Alerta',
          content: 'No se ha seleccionado una plantilla!',
          
          icon: 'fa fa-close',
          type: 'blue',
          buttons: {
              confirm: {
                  text: 'OK',
                  btnClass: 'btn-blue',
              }
          }
      });
			console.log($("#errorsubida").attr("style"));
		}else{	
  			window.location.href = "descarga.php?archivo=" + dsc;
  		}
  		setTimeout('borra()',60);
	});

	$('#ceirratipo').on('click', function(e){  
  		window.location.href = "lllistado_step.php?idr=<?php echo $_SESSION['id'];?>";
	});
</script>

<script type="text/javascript">
	$(document).ready(function() {
        $.ajax({
                type: "POST",
                url: "getmacroproceso.php",
                success: function(response)
                {
                    $('.macroproceso select').html(response).fadeIn();
                }
        });
    });

	$(document).ready(function() {
        $.ajax({
                type: "POST",
                url: "getunidad.php",
                success: function(response)
                {
                    $('.divisiona select').html(response).fadeIn();
                }
        });
    });

    $(document).ready(function() {
        $.ajax({
                type: "POST",
                url: "getsolucionc.php",
                success: function(response)
                {
                    $('.solucionc select').html(response).fadeIn();
                }
        });
    });

    $(document).ready(function() {
        $.ajax({
                type: "POST",
                url: "gettac.php",
                success: function(response)
                {
                    $('.tacontratar select').html(response).fadeIn();
                }
        });
    });

     $('#macro').on('change', function(){
    	var valor_rut = $('#macro').val();
    	 $.ajax({
                type: "POST",
                data:{macro:valor_rut},
                url: "getproceso.php",
                success: function(response)
                {
                    $('.proceso select').html(response).fadeIn()
                }
        });    
  });
      $('#diva').on('change', function(){
    	var valor_rut = $('#diva').val();
    	 $.ajax({
                type: "POST",
                data:{macro:valor_rut},
                url: "getservicio.php",
                success: function(response)
                {
                    $('.servicioa select').html(response).fadeIn()
                }
        });    
  });

</script>
<script type="text/javascript">

    var s1;
    $(function () {
        //if you have any radio selected by default
        s1 = $('[name="rdioec"]:checked').val();
    });
    $(document).on('click', '[name="rdioec"]', function () {
        s1 = $(this).val();
        //alert(s1);
        if (s1 =="Procede") {
        	$('#seval').removeAttr("required");
        	$('#eval').attr("required","required");
        }else if(s1 =="Procede Con Observación"){
			$('#seval').attr("required","required");
			$('#eval').attr("required","required");
        }else{
			$('#seval').attr("required","required");
			$('#eval').removeAttr("required");
        }
    });

    var s2;
    $(function () {
        //if you have any radio selected by default
        s2 = $('[name="rdiocna"]:checked').val();
    });
    $(document).on('click', '[name="rdiocna"]', function () {
        s2 = $(this).val();
        //alert(s2);
        if (s2 =="Procede") {
        	$('#sconst').removeAttr("required");
        	$('#const').attr("required","required");
        }else if(s2 =="Procede Con Observación"){
			$('#sconst').attr("required","required");
			$('#const').attr("required","required");
        }else{
			$('#sconst').attr("required","required");
			$('#const').removeAttr("required");
        }
    });

    var s3;
    $(function () {
        //if you have any radio selected by default
        s3 = $('[name="rdioplaft"]:checked').val();
    });
    $(document).on('click', '[name="rdioplaft"]', function () {
        s3 = $(this).val();
       // alert(s3);
       if (s3 =="Procede") {
        	$('#splaft').removeAttr("required");
        	$('#plaft').attr("required","required");
        }else if(s3 =="Procede Con Observación"){
			$('#splaft').attr("required","required");
			$('#plaft').attr("required","required");
        }else{
			$('#splaft').attr("required","required");
			$('#plaft').removeAttr("required");
        }
    });

    var s4;
    $(function () {
        //if you have any radio selected by default
        s4 = $('[name="rdiosst"]:checked').val();
    });
    $(document).on('click', '[name="rdiosst"]', function () {
        s4 = $(this).val();
       // alert(s4);
       if (s4 =="Procede") {
        	$('#ssst').removeAttr("required");
        	$('#sst').attr("required","required");
        }else if(s4 =="Procede Con Observación"){
			$('#ssst').attr("required","required");
			$('#sst').attr("required","required");
        }else{
			$('#ssst').attr("required","required");
			$('#sst').removeAttr("required");
        }
    });

    var s5;
    $(function () {
        //if you have any radio selected by default
        s5 = $('[name="rdiodc"]:checked').val();
    });
    $(document).on('click', '[name="rdiodc"]', function () {
        s5 = $(this).val();
       // alert(s5);
       if (s5 =="Procede") {
        	$('#scumpl').removeAttr("required");
        	$('#cumpl').attr("required","required");
        }else if(s5 =="Procede Con Observación"){
			$('#scumpl').attr("required","required");
			$('#cumpl').attr("required","required");
        }else{
			$('#scumpl').attr("required","required");
			$('#cumpl').removeAttr("required");
        }
    });

    var s6;
    $(function () {
        //if you have any radio selected by default
        s6 = $('[name="rdioh"]:checked').val();
    });
    $(document).on('click', '[name="rdioh"]', function () {
        s6 = $(this).val();
        //alert(s6);
        if (s6 =="Procede") {
        	$('#shomo').removeAttr("required");
        	$('#homo').attr("required","required");
        }else if(s6 =="Procede Con Observación"){
			$('#shomo').attr("required","required");
			$('#homo').attr("required","required");
        }else{
			$('#shomo').attr("required","required");
			$('#homo').removeAttr("required");
        }
    });

</script>

<script>
	
$(document).ready(function(){

	$('#formtab1').on('submit', function(e){  
	 	e.preventDefault(); 
	 	$.confirm({
          title: 'Alerta!',
          content: '¿Está seguro que desea solicitar el requerimiento?',
          icon: 'fa fa-info',
          type: 'blue',
          buttons: {
          	cancelar: {
                  text: 'No',
                  btnClass: 'btn-red',
              },
              aceptar: {
                  text: 'Si',
                  btnClass: 'btn-blue',
                  action: function() { 
		    $.ajax({  
			    url:"insert.php",  
			    method:"POST",  
			    data:$('#formtab1').serialize(), 
			    success: function (resp){
			    	$("#solicita1").attr("style", "display:none")
			    	console.log(resp)
			    	if (resp.trim() =="correcto") {
			    	 
			    	 $("#error").attr("class", "alert alert-danger display-block")
			    	 $("#correcto").attr("class", "alert alert-success display-block")
			    	 $("#siguiente").attr("style", "display:none;float: right;")
			    	 $("#atras").attr("style", "display:none")
			    	 $("#fin").attr("style", "display:none")
			    	 $("#solicita1").attr("style", "display:none")
			    	 $("#error").attr("class", "alert alert-danger display-none")
			    	 comm()
			    	 aprobacion_correo()
			    	}else{
			    	
			    	 $("#siguiente").attr("style", "display:none")
			    	 $("#atras").attr("style", "display:none")
			    	 $("#fin").attr("style", "display:none")
			    	 $("#error").attr("class", "alert alert-danger display-none")
			    	 $("#correcto").attr("class", "alert alert-success display-block")
			    	 $("#solicita1").attr("style", "display:block")
			    	}
			    },
			    error: function (jqXHR, estado, error){	
			    	console.log(estado)
			    	console.log(error)
			    },
			    complete: function (jqXHR, estado){
			    	console.log(estado)
			    },
		   });  
  			}
                                
          }
          
      }
   })
		     
   });
	function comm(){
		  var comentario = $('#comm').val();
		$.ajax({
			   url:"comm1.php",
			   method:"POST",
			   data:{comentario:comentario},
			   success:function(data){
			   	if (data=="incorrecto") {
			   		console.log("correo no enviado");
			   	}else{
			   		console.log("correo enviado");
			   	}
			   
			   },
			    error: function (jqXHR, estado, error){	
			    	console.log(estado)
			    	console.log(error)
			    },
			    complete: function (jqXHR, estado){
			    	console.log(estado)
			    },
			   });
	}
	function tipo_p(){
		$.ajax({
			   url:"tipo_proveedor.php",
			   method:"POST",
			   success:function(data){
			    $('#contenido_tipo_proveedor').html(data);
			    $('#tipo_proveedor').modal('show');
			   }
			   });
	}


	function aprobacion_correo(){
		var comentario = $('#comm').val();
		console.log("va a mandar correo");
		$.ajax({
			   url:"correo.php",
			   method:"POST",
			   data:{com: comentario},
			   success:function(data){
			   	if (data =="incorrecto") {
			   		console.log("correo no enviado");
			   	}else{
			   		console.log("correo enviado");
			   	}
			   
			   },
			    error: function (jqXHR, estado, error){	
			    	console.log(estado)
			    	console.log(error)
			    },
			    complete: function (jqXHR, estado){
			    	console.log(estado)
			    },
			   });
	}
//qwerty
	$('#formtab2').on('submit', function(e){  
	 	e.preventDefault();
	 	  $.confirm({
	      title: 'Alerta!',
	      content: '¿Está seguro que la información ingresada es la correcta?',
	      icon: 'fa fa-info',
	      type: 'blue',
	      buttons: {
	          cancelar: {
	              text: 'No',
	              btnClass: 'btn-red',
	          },
	          aceptar: {
	              text: 'Si',
	              btnClass: 'btn-blue',
	              action: function() {
	                $.ajax({  
				    url:"insert2.php",  
				    method:"POST",  
				    data:$('#formtab2').serialize(), 
				    success: function (resp){

				    	console.log(resp)
				    	if (resp.trim()=="correcto") {
				    	 $("#error").attr("class", "alert alert-danger display-none")
				    	 $("#form").attr("class", "alert alert-success display-block")
				    	 $("#siguiente1").attr("style", "display:block;float: right;")
				    	 $("#siguiente2").attr("style", "display:block;float: right;")
				    	 $("#atras1").attr("style", "display:block")
				    	 $("#fin2").attr("style", "display:none")
				    	 $("#reg").attr("style", "display:none")
				    	 $("#reg1").attr("style", "display:none")
				    	 $("#reg2").attr("style", "display:none")
				    	 $("#siguiente1").attr("value", "iniciado")
				    	 tipo_p()
				    	}else{
				    	 $("#siguiente1").attr("style", "display:none")
				    	 $("#atras1").attr("style", "display:block")
				    	 $("#fin2").attr("style", "display:none")
				    	 $("#error").attr("class", "alert alert-danger display-none")
				    	 $("#form").attr("class", "alert alert-success display-block")
				    	}
				    },
				    error: function (jqXHR, estado, error){	
				    	console.log(estado)
				    	console.log(error)
				    },
				    complete: function (jqXHR, estado){
				    	console.log(estado)
				    },

			   		});  
	             }
	            
	          }
	      }
   	})  
		     
   });

	$('#formtab3').on('submit', function(e){  
	 	e.preventDefault();
	 	$.confirm({
      title: 'Alerta!',
      content: '¿Está seguro que la información ingresada es la correcta?',
      icon: 'fa fa-info',
      type: 'blue',
      buttons: {
          cancelar: {
              text: 'No',
              btnClass: 'btn-red',
          },
          aceptar: {
              text: 'Si',
              btnClass: 'btn-blue',
              action: function() {
                   $.ajax({  
			    url:"insert3.php",  
			    method:"POST",  
			    data:$('#formtab3').serialize(), 
			    success: function (resp){

			    	console.log(resp)
			    	if (resp.trim()=="correcto") {
			    	 $("#error").attr("class", "alert alert-danger display-none")
			    	 $("#evaluac").attr("class", "alert alert-success display-block")
			    	 $("#siguiente2").attr("style", "display:block;float: right;")
			    	 $("#atras2").attr("style", "display:block")
			    	 $("#fin").attr("style", "display:none")
			    	 $("#fin").attr("style", "display:none")
			    	 $("#gistro").attr("style", "display:none")
			    	 cotizacion()
			    	}else{
			    	 $("#siguiente2").attr("style", "display:none")
			    	 $("#atras2").attr("style", "display:block")
			    	 $("#fin").attr("style", "display:none")
			    	 $("#error").attr("class", "alert alert-danger display-none")
			    	 $("#evaluac").attr("class", "alert alert-success display-block")
			    	 
			    	}
			    },
			    error: function (jqXHR, estado, error){	
			    	console.log(estado)
			    	console.log(error)
			    },
			    complete: function (jqXHR, estado){
			    	console.log(estado)
			    },

		   		}); 
             }
            
          }
      }
   })  
		     
   });
	function cotizacion(){
		var formData = new FormData($('#formtab3')[0]); 
		    $.ajax({  
			    url:"filecotizacion.php",  
			    method:"POST",  
			    data:formData, 
			    cache: false,
            contentType: false,
            processData: false,
			    success: function (resp){
			    	console.log(resp)
			    	if (resp.trim() =='true') {
			    		console.log("cargado con exito");
			    		window.location.href = "llistado_step.php?idr=<?php echo $_SESSION['id'];?>";
			    	}else{
			    		console.log("no se cargo con exito");
			    	}
			    },
			    error: function (jqXHR, estado, error){	
			    	console.log(estado)
			    	console.log(error)
			    },
			    complete: function (jqXHR, estado){
			    	console.log(estado)
			    },

		   }); 
	}

	function docprov(){
	    $.ajax({  
	    url:"insert4.php",  
	    method:"POST",  
	    data:$('#formtab4').serialize(), 
	    success: function (resp){
	    	console.log(resp)
	    },
	    error: function (jqXHR, estado, error){	
	    	console.log(estado)
	    	console.log(error)
	    },
	    complete: function (jqXHR, estado){
	    	console.log(estado)
	    },

   		}); 
	}

	function contrato(){
	    $.ajax({  
	    url:"insert6.php",  
	    method:"POST",  
	    data:$('#formtab6').serialize(), 
	    success: function (resp){
	    	correorevision();
	    	console.log(resp)
	    },
	    error: function (jqXHR, estado, error){	
	    	console.log(estado)
	    	console.log(error)
	    },
	    complete: function (jqXHR, estado){
	    	console.log(estado)
	    },

   		}); 
	}

		function correorevision(){
	    $.ajax({  
	    url:"correorev.php",  
	    method:"POST",  
	    data:$('#formtab6').serialize(), 
	    success: function (resp){
	    	console.log(resp)
	    },
	    error: function (jqXHR, estado, error){	
	    	console.log(estado)
	    	console.log(error)
	    },
	    complete: function (jqXHR, estado){
	    	console.log(estado)
	    },

   		}); 
	}

	function contratofirmado(){
	    $.ajax({  
	    url:"contratofirmado.php",  
	    method:"POST",  
	    data:$('#formtab7').serialize(), 
	    success: function (resp){
	    	correorevisionfirmado();
	    	console.log(resp);
	    },
	    error: function (jqXHR, estado, error){	
	    	console.log(estado)
	    	console.log(error)
	    },
	    complete: function (jqXHR, estado){
	    	console.log(estado)
	    },

   		}); 
	}

		function correorevisionfirmado(){
	    $.ajax({  
	    url:"correorevfirmado.php",  
	    method:"POST",  
	    data:$('#formtab7').serialize(), 
	    success: function (resp){
	    	if (resp.trim() =="incorrecto") {
	    		console.log("correo no enviado");
	    	}else{
	    		console.log("correo enviado");
	    	}
	    },
	    error: function (jqXHR, estado, error){	
	    	console.log(estado)
	    	console.log(error)
	    },
	    complete: function (jqXHR, estado){
	    	console.log(estado)
	    },

   		}); 
	}

	$('#formtab7').on('submit', function(e){ 
	var formData = new FormData($('#formtab7')[0]); 
	 	e.preventDefault(); 

	 	$.confirm({
          title: 'Alerta!',
          content: '¿Está seguro que desea enviar la información?',
          icon: 'fa fa-info',
          type: 'blue',
          buttons: {
          	cancelar: {
                  text: 'No',
                  btnClass: 'btn-red',
              },
              aceptar: {
                  text: 'Si',
                  btnClass: 'btn-blue',
                  action: function() { 
		   $.ajax({  
			    url:"filecontratofirmado.php",  
			    method:"POST",  
			    data:formData, 
			    cache: false,
            contentType: false,
            processData: false,
			    success: function (resp){
			    	console.log(resp)
			    	if (resp.trim() =='true') {
			    		$('#enviar').attr("style","display:none;");
			    		resultadoOk();
			    		contratofirmado();
			    	}else{
			    		resultadoErroneo();
			    	}
			    },
			    error: function (jqXHR, estado, error){	
			    	console.log(estado)
			    	console.log(error)
			    },
			    complete: function (jqXHR, estado){
			    	console.log(estado)
			    },

		   });   
  			}
                                
          }
          
      }
   })

		     
   });
	
	$('#formtab4').on('submit', function(e){ 
	console.log("enviando formulario");
	var formData = new FormData($('#formtab4')[0]); 
	 	e.preventDefault(); 

	 	$.confirm({
          title: 'Alerta!',
          content: '¿Está seguro que desea enviar la documentación?',
          icon: 'fa fa-info',
          type: 'blue',
          buttons: {
          	cancelar: {
                  text: 'No',
                  btnClass: 'btn-red',
              },
              aceptar: {
                  text: 'Si',
                  btnClass: 'btn-blue',
                  action: function() { 
		    $.ajax({  
			    url:"filedocumentacion.php",  
			    method:"POST",  
			    data:formData, 
			    cache: false,
            	contentType: false,
           		processData: false,
			    success: function (resp){
			    	console.log(resp)
			    	if (resp.trim() =='true') {
			    		resultadoOk();
			    		docprov();
			    		$("#siguiente3").attr("style", "display:block;float: right;")
			    	 	$("#atras3").attr("style", "display:block")
			    	 	$("#upload").attr("style", "display:none")
			    	}else{
			    		resultadoErroneo();
			    		$("#siguiente3").attr("style", "display:none")
			    	}
			    },
			    error: function (jqXHR, estado, error){	
			    	console.log(estado)
			    	console.log(error)
			    },
			    complete: function (jqXHR, estado){
			    	console.log(estado)
			    },

		   });   
  			}
                                
          }
          
      }
   })

		    
   });

	$('#formtab6').on('submit', function(e){ 
	var formData = new FormData($('#formtab6')[0]); 
	 	e.preventDefault(); 

	 	$.confirm({
          title: 'Alerta!',
          content: '¿Está seguro que desea enviar la documentación?',
          icon: 'fa fa-info',
          type: 'blue',
          buttons: {
          	cancelar: {
                  text: 'No',
                  btnClass: 'btn-red',
              },
              aceptar: {
                  text: 'Si',
                  btnClass: 'btn-blue',
                  action: function() { 
		   $.ajax({  
			    url:"fileup.php",  
			    method:"POST",  
			    data:formData, 
			    cache: false,
            contentType: false,
            processData: false,
			    success: function (resp){
			    	console.log(resp)
			    	if (resp.trim() =='true') {
			    		$('#enviar').attr("style","display:none;");
			    		resultadoOk();
			    		contrato();
			    	}else{
			    		resultadoErroneo();
			    	}
			    },
			    error: function (jqXHR, estado, error){	
			    	console.log(estado)
			    	console.log(error)
			    },
			    complete: function (jqXHR, estado){
			    	console.log(estado)
			    },

		   });   
  			}
                                
          }
          
      }
   })

		     
   });

 	$('#guardar').on('click',function(){
		console.log("click");
	});

	$('#critform').on('submit', function(e){  
	 	e.preventDefault();
		    $.ajax({  
			    url:"actualizacriterio.php",  
			    method:"POST",  
			    data:$('#critform').serialize(),
			    beforeSend: function(){
			      $('#insert').attr('value', "Ver criterios generados");
			    }, 
			    success: function (rr){
			    	console.log(rr)
			    	if (rr.trim() =='incorrecto') {
			    		console.log("no enviado")
			    	}else{
			    		console.log("enviado")	
			    	 	$('#valoraciones').modal('hide')
			    	}
			    },
			    error: function (jqXHR, estado, error){	
			    	console.log(estado)
			    	console.log(error)
			    },
			    complete: function (jqXHR, estado){
			    	console.log(estado)
			    },

		   }); 
   });

		$('#provform').on('submit', function(e){  
	 	e.preventDefault();
		    $.ajax({  
			    url:"agregarproveedor.php",  
			    method:"POST",  
			    data:$('#provform').serialize(),
			    success: function (rr){
			    	console.log(rr)
			    	if (rr.trim() =='existe') {
			    		$('#controlproveedor').val("")
			    		console.log($('#controlproveedor').val())
			    		 $.alert({
                              title: 'Error',
                              content: 'El RUC ingresado ya existe!',
                              
                              icon: 'fa fa-close',
                              type: 'red',
                              buttons: {
                                  confirm: {
                                      text: 'OK',
                                      btnClass: 'btn-red',
                                  }
                              }
                          });	
			    	}else{
			    		console.log("correcto")
			    		$('#controlproveedor').val("ok")	
			    	 	$('#provve').modal('hide')
		    	 		 $.alert({
                              title: 'Confirmación',
                              content: 'Proveedor agregado con Éxito!',
                              
                              icon: 'fa fa-send',
                              type: 'green',
                              buttons: {
                                  confirm: {
                                      text: 'OK',
                                      btnClass: 'btn-blue',
                                      action: function(){
                                      	window.location.href = "llistado_step.php?idr=<?php echo $_SESSION['id'];?>";
                                      }
                                  }
                              }
                          });

			    	}
			    },
			    error: function (jqXHR, estado, error){	
			    	console.log(estado)
			    	console.log(error)
			    },
			    complete: function (jqXHR, estado){
			    	console.log(estado)
			    },

		   }); 
   });

	$('#valorform').on('submit', function(e){  
	 	e.preventDefault();
		    $.ajax({  
			    url:"actualizavaloracion.php",  
			    method:"POST",  
			    data:$('#valorform').serialize(),
			    beforeSend: function(){
			    }, 
			    success: function (rr){
			    	console.log(rr)
			    	if (rr.trim() =='incorrecto') {
			    		console.log("no enviado")
			    	}else{
			    		if ($('#tmp').val() == "evaluador") {
			    	 		$("#evaluador").html("EVALUADO");
			    	 		$("#evaluador").attr("class", "btn green");
			    	 		$("#evaluador").attr("style", "left: -3%;padding-left: 9px;padding-right: 9px;");
			    	 	}else if($('#tmp').val() == "evaluador1"){
			    	 		$('#evaluador1').html("EVALUADO");
			    	 		$("#evaluador1").attr("class", "btn green");
			    	 		$("#evaluador1").attr("style", "left: -3%;padding-left: 9px;padding-right: 9px;");
			    	 	}else if($('#tmp').val() == "evaluador2"){
			    	 		$('#evaluador2').html("EVALUADO");
			    	 		$("#evaluador2").attr("class", "btn green");
			    	 		$("#evaluador2").attr("style", "left: -3%;padding-left: 9px;padding-right: 9px;");
			    	 	}else if($('#tmp').val() == "evaluador3"){
			    	 		$('#evaluador3').html("EVALUADO");
			    	 		$("#evaluador3").attr("class", "btn green");
			    	 		$("#evaluador3").attr("style", "left: -3%;padding-left: 9px;padding-right: 9px;");
			    	 	}else {
			    	 		$('#evaluador4').html("EVALUADO");
			    	 		$("#evaluador4").attr("class", "btn green");
			    	 		$("#evaluador4").attr("style", "left: -3%;padding-left: 9px;padding-right: 9px;");
			    	 	}
			    	 	console.log($('#tmp').val());
			    		console.log("enviado")
			    	 	$('#valor').modal('hide')

			    	 	

			    	}
			    	completar();
			    },
			    error: function (jqXHR, estado, error){	
			    	console.log(estado)
			    	console.log(error)
			    },
			    complete: function (jqXHR, estado){
			    	console.log(estado)
			    },

		   }); 
   });

$('#valorforma').on('submit', function(e){  
	 	e.preventDefault();
		    $.ajax({  
			    url:"actualizavaloracion.php",  
			    method:"POST",  
			    data:$('#valorforma').serialize(),
			    beforeSend: function(){
			    }, 
			    success: function (rr){
			    	console.log(rr)
			    	if (rr.trim() =='incorrecto') {
			    		console.log("no enviado")
			    	}else{
			    		if ($('#tmp').val() == "evaluador") {
			    	 		$("#evaluador").html("EVALUADO");
			    	 		$("#evaluador").attr("class", "btn green");
			    	 		$("#evaluador").attr("style", "left: -3%;padding-left: 9px;padding-right: 9px;");
			    	 	}else if($('#tmp').val() == "evaluador1"){
			    	 		$('#evaluador1').html("EVALUADO");
			    	 		$("#evaluador1").attr("class", "btn green");
			    	 		$("#evaluador1").attr("style", "left: -3%;padding-left: 9px;padding-right: 9px;");
			    	 	}else if($('#tmp').val() == "evaluador2"){
			    	 		$('#evaluador2').html("EVALUADO");
			    	 		$("#evaluador2").attr("class", "btn green");
			    	 		$("#evaluador2").attr("style", "left: -3%;padding-left: 9px;padding-right: 9px;");
			    	 	}else if($('#tmp').val() == "evaluador3"){
			    	 		$('#evaluador3').html("EVALUADO");
			    	 		$("#evaluador3").attr("class", "btn green");
			    	 		$("#evaluador3").attr("style", "left: -3%;padding-left: 9px;padding-right: 9px;");
			    	 	}else {
			    	 		$('#evaluador4').html("EVALUADO");
			    	 		$("#evaluador4").attr("class", "btn green");
			    	 		$("#evaluador4").attr("style", "left: -3%;padding-left: 9px;padding-right: 9px;");
			    	 	}
			    	 	console.log($('#tmp').val());
			    		console.log("enviado")
			    	 	$('#valora').modal('hide')

			    	 	

			    	}
			    	completar();
			    },
			    error: function (jqXHR, estado, error){	
			    	console.log(estado)
			    	console.log(error)
			    },
			    complete: function (jqXHR, estado){
			    	console.log(estado)
			    },

		   }); 
   });

	$('#critform1').on('submit', function(e){  
	 	e.preventDefault();
		    $.ajax({  
			    url:"actualizacriterio.php",  
			    method:"POST",  
			    data:$('#critform1').serialize(),
			    beforeSend: function(){
			      
			    }, 
			    success: function (rr){
			    	console.log(rr)
			    	if (rr.trim() =='incorrecto') {
			    		console.log("no enviado")
			    	}else{
			    		console.log("enviado")
			    	 	$('#criterios').modal('hide')
			    	 	$('#registrar').attr('value', "Actualizar");
			    	 	$('#tituloact').html("Ver Criterios");
			    	 	$('#elcrit').html("Ver Criterios");
			    	 	
			    	}
			    },
			    error: function (jqXHR, estado, error){	
			    	console.log(estado)
			    	console.log(error)
			    },
			    complete: function (jqXHR, estado){
			    	console.log(estado)
			    },

		   }); 
   });

	$('#siguiente').on('click',function(e){
		var $pwidth=$('.active').attr("id");
			console.log($pwidth)
			switch ($pwidth) {
		    case 'l1':
		        $("#tab1").attr("class", "tab-pane")
				$("#tab2").attr("class", "tab-pane active")
				$("#l2").attr("class", "active")
				$("#l1").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
				$("#atras").attr("style","display:block")
				$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
			console.log($pwidth)
		        break;

		    case 'l2':
		        $("#tab2").attr("class", "tab-pane") 
				$("#tab3").attr("class", "tab-pane active")
				$("#l3").attr("class", "active")
				$("#l2").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
				$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
				console.log($pwidth)
		        break;

		    case 'l3':
		    	$("#tab3").attr("class", "tab-pane") 
				$("#tab4").attr("class", "tab-pane active")
				$("#l4").attr("class", "active")
				$("#l3").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        console.log($pwidth)
		        break;

	        case 'l4':
	       		$("#tab4").attr("class", "tab-pane") 
				$("#tab5").attr("class", "tab-pane active")
				$("#l5").attr("class", "active")
				$("#l4").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        console.log($pwidth)
		        break;

		    case 'l5':
		    	$("#tab5").attr("class", "tab-pane") 
				$("#tab6").attr("class", "tab-pane active")
				$("#l6").attr("class", "active")
				$("#l5").attr("class", "done")
				$("#siguiente").attr("style","display:none")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        console.log($pwidth)
		        break;
			}
    });

    $('#siguiente1').on('click',function(e){
		var $pwidth=$('.active').attr("id");
			console.log($pwidth)
			switch ($pwidth) {
		    case 'l1':
		        $("#tab1").attr("class", "tab-pane")
				$("#tab2").attr("class", "tab-pane active")
				$("#l2").attr("class", "active")
				$("#l1").attr("class", "done")
				$("#siguiente1").attr("style","display:block;float: right;")
				$("#atras1").attr("style","display:block")
				$("#error").attr("class", "alert alert-danger display-none")
			    $("#form").attr("class", "alert alert-success display-none")
			console.log($pwidth)
		        break;

		    case 'l2':
		        $("#tab2").attr("class", "tab-pane") 
				$("#tab3").attr("class", "tab-pane active")
				$("#l3").attr("class", "active")
				$("#l2").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
				$("#error").attr("class", "alert alert-danger display-none")
			    $("#form").attr("class", "alert alert-success display-none")
				console.log($pwidth)
		        break;

		    case 'l3':
		    	$("#tab3").attr("class", "tab-pane") 
				$("#tab4").attr("class", "tab-pane active")
				$("#l4").attr("class", "active")
				$("#l3").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#form").attr("class", "alert alert-success display-none")
		        console.log($pwidth)
		        break;

	        case 'l4':
	       		$("#tab4").attr("class", "tab-pane") 
				$("#tab5").attr("class", "tab-pane active")
				$("#l5").attr("class", "active")
				$("#l4").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#form").attr("class", "alert alert-success display-none")
		        console.log($pwidth)
		        break;

		    case 'l5':
		    	$("#tab5").attr("class", "tab-pane") 
				$("#tab6").attr("class", "tab-pane active")
				$("#l6").attr("class", "active")
				$("#l5").attr("class", "done")
				$("#siguiente").attr("style","display:none")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#form").attr("class", "alert alert-success display-none")
		        console.log($pwidth)
		        break;
			}
			console.log($(this).attr("value"));
			if ($(this).attr("value") == "iniciado") {
				window.location.href = "llistado_step.php?idr=<?php echo $_SESSION['id'];?>";
			}
    });

    $('#siguiente2').on('click',function(e){
		var $pwidth=$('.active').attr("id");
			console.log($pwidth)
			switch ($pwidth) {
		    case 'l1':
		        $("#tab1").attr("class", "tab-pane")
				$("#tab2").attr("class", "tab-pane active")
				$("#l2").attr("class", "active")
				$("#l1").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
				$("#atras").attr("style","display:block")
				$("#error").attr("class", "alert alert-danger display-none")
			    $("#evaluac").attr("class", "alert alert-success display-none")
			console.log($pwidth)
		        break;

		    case 'l2':
		        $("#tab2").attr("class", "tab-pane") 
				$("#tab3").attr("class", "tab-pane active")
				$("#l3").attr("class", "active")
				$("#l2").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
				$("#error").attr("class", "alert alert-danger display-none")
			    $("#evaluac").attr("class", "alert alert-success display-none")
				console.log($pwidth)
		        break;

		    case 'l3':
		    	$("#tab3").attr("class", "tab-pane") 
				$("#tab4").attr("class", "tab-pane active")
				$("#l4").attr("class", "active")
				$("#l3").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#evaluac").attr("class", "alert alert-success display-none")
		        console.log($pwidth)
		        break;

	        case 'l4':
	       		$("#tab4").attr("class", "tab-pane") 
				$("#tab5").attr("class", "tab-pane active")
				$("#l5").attr("class", "active")
				$("#l4").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#evaluac").attr("class", "alert alert-success display-none")
		        console.log($pwidth)
		        break;

		    case 'l5':
		    	$("#tab5").attr("class", "tab-pane") 
				$("#tab6").attr("class", "tab-pane active")
				$("#l6").attr("class", "active")
				$("#l5").attr("class", "done")
				$("#siguiente").attr("style","display:none")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#evaluac").attr("class", "alert alert-success display-none")
		        console.log($pwidth)
		        break;
			}
    });

    $('#siguiente3').on('click',function(e){
		var $pwidth=$('.active').attr("id");
			console.log($pwidth)
			switch ($pwidth) {
		    case 'l1':
		        $("#tab1").attr("class", "tab-pane")
				$("#tab2").attr("class", "tab-pane active")
				$("#l2").attr("class", "active")
				$("#l1").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
				$("#atras").attr("style","display:block")
				$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
			    $("#subido").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
			console.log($pwidth)
		        break;

		    case 'l2':
		        $("#tab2").attr("class", "tab-pane") 
				$("#tab3").attr("class", "tab-pane active")
				$("#l3").attr("class", "active")
				$("#l2").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
				$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
			    $("#subido").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
				console.log($pwidth)
		        break;

		    case 'l3':
		    	$("#tab3").attr("class", "tab-pane") 
				$("#tab4").attr("class", "tab-pane active")
				$("#l4").attr("class", "active")
				$("#l3").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
			    $("#subido").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
		        console.log($pwidth)
		        break;

	        case 'l4':
	       		$("#tab4").attr("class", "tab-pane") 
				$("#tab5").attr("class", "tab-pane active")
				$("#l5").attr("class", "active")
				$("#l4").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
			    $("#subido").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
		        console.log($pwidth)
		        break;

		    case 'l5':
		    	$("#tab5").attr("class", "tab-pane") 
				$("#tab6").attr("class", "tab-pane active")
				$("#l6").attr("class", "active")
				$("#l5").attr("class", "done")
				$("#siguiente").attr("style","display:none")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
			    $("#subido").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
		        console.log($pwidth)
		        break;
			}
    });

    $('#siguiente4').on('click',function(e){
		var $pwidth=$('.active').attr("id");
			console.log($pwidth)
			switch ($pwidth) {
		    case 'l1':
		        $("#tab1").attr("class", "tab-pane")
				$("#tab2").attr("class", "tab-pane active")
				$("#l2").attr("class", "active")
				$("#l1").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
				$("#atras").attr("style","display:block")
				$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
			console.log($pwidth)
		        break;

		    case 'l2':
		        $("#tab2").attr("class", "tab-pane") 
				$("#tab3").attr("class", "tab-pane active")
				$("#l3").attr("class", "active")
				$("#l2").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
				$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
				console.log($pwidth)
		        break;

		    case 'l3':
		    	$("#tab3").attr("class", "tab-pane") 
				$("#tab4").attr("class", "tab-pane active")
				$("#l4").attr("class", "active")
				$("#l3").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        console.log($pwidth)
		        break;

	        case 'l4':
	       		$("#tab4").attr("class", "tab-pane") 
				$("#tab5").attr("class", "tab-pane active")
				$("#l5").attr("class", "active")
				$("#l4").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        console.log($pwidth)
		        break;

		    case 'l5':
		    	$("#tab5").attr("class", "tab-pane") 
				$("#tab6").attr("class", "tab-pane active")
				$("#l6").attr("class", "active")
				$("#l5").attr("class", "done")
				$("#siguiente").attr("style","display:none")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        console.log($pwidth)
		        break;
			}
    });

    $('#siguiente5').on('click',function(e){
		var $pwidth=$('.active').attr("id");
			console.log($pwidth)
			switch ($pwidth) {
		    case 'l1':
		        $("#tab1").attr("class", "tab-pane")
				$("#tab2").attr("class", "tab-pane active")
				$("#l2").attr("class", "active")
				$("#l1").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
				$("#atras").attr("style","display:block")
				$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
			    $("#subido").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
			console.log($pwidth)
		        break;

		    case 'l2':
		        $("#tab2").attr("class", "tab-pane") 
				$("#tab3").attr("class", "tab-pane active")
				$("#l3").attr("class", "active")
				$("#l2").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
				$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
			    $("#subido").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
				console.log($pwidth)
		        break;

		    case 'l3':
		    	$("#tab3").attr("class", "tab-pane") 
				$("#tab4").attr("class", "tab-pane active")
				$("#l4").attr("class", "active")
				$("#l3").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
			    $("#subido").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
		        console.log($pwidth)
		        break;

	        case 'l4':
	       		$("#tab4").attr("class", "tab-pane") 
				$("#tab5").attr("class", "tab-pane active")
				$("#l5").attr("class", "active")
				$("#l4").attr("class", "done")
				$("#siguiente").attr("style","display:block;float: right;")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
			    $("#subido").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
		        console.log($pwidth)
		        break;

		    case 'l5':
		    	$("#tab5").attr("class", "tab-pane") 
				$("#tab6").attr("class", "tab-pane active")
				$("#l6").attr("class", "active")
				$("#l5").attr("class", "done")
				$("#siguiente").attr("style","display:none")
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
			    $("#subido").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
		        console.log($pwidth)
		        break;
			}
    });


    $('#atras').on('click',function(e){
		var $pwidth=$('.active').attr("id");
			console.log($pwidth)
			switch ($pwidth) {
		    case 'l2':
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		    	$("#tab2").attr("class", "tab-pane")
				$("#tab1").attr("class", "tab-pane active")
				$("#l1").attr("class", "active")
				$("#l2").attr("class", "none")
				$("#atras").attr("style","display:none")
			console.log($pwidth)
		        break;

		    case 'l3':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab3").attr("class", "tab-pane") 
				$("#tab2").attr("class", "tab-pane active")
				$("#l2").attr("class", "active")
				$("#l3").attr("class", "none")
				$("#atras").attr("style","display:block")
				console.log($pwidth)
		        break;

		   case 'l4':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab4").attr("class", "tab-pane") 
				$("#tab3").attr("class", "tab-pane active")
				$("#l3").attr("class", "active")
				$("#l4").attr("class", "none")
				$("#atras").attr("style","display:block")
				console.log($pwidth)
		        break;

		    case 'l5':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab5").attr("class", "tab-pane") 
				$("#tab4").attr("class", "tab-pane active")
				$("#l4").attr("class", "active")
				$("#l5").attr("class", "none")
				$("#atras").attr("style","display:block")
				console.log($pwidth)
		        break;

		    case 'l6':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab6").attr("class", "tab-pane") 
				$("#tab5").attr("class", "tab-pane active")
				$("#l5").attr("class", "active")
				$("#l6").attr("class", "none")
				$("#atras").attr("style","display:block")
				$("#siguiente").attr("style","display:block;float: right;")
				console.log($pwidth)
		        break;

			}
    });

    $('#atras1').on('click',function(e){
		var $pwidth=$('.active').attr("id");
			console.log($pwidth)
			switch ($pwidth) {
		    case 'l2':
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		    	$("#tab2").attr("class", "tab-pane")
				$("#tab1").attr("class", "tab-pane active")
				$("#l1").attr("class", "active")
				$("#l2").attr("class", "none")
				$("#atras").attr("style","display:none")
			console.log($pwidth)
		        break;

		    case 'l3':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab3").attr("class", "tab-pane") 
				$("#tab2").attr("class", "tab-pane active")
				$("#l2").attr("class", "active")
				$("#l3").attr("class", "none")
				$("#atras").attr("style","display:block")
				console.log($pwidth)
		        break;

		   case 'l4':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab4").attr("class", "tab-pane") 
				$("#tab3").attr("class", "tab-pane active")
				$("#l3").attr("class", "active")
				$("#l4").attr("class", "none")
				$("#atras").attr("style","display:block")
				console.log($pwidth)
		        break;

		    case 'l5':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab5").attr("class", "tab-pane") 
				$("#tab4").attr("class", "tab-pane active")
				$("#l4").attr("class", "active")
				$("#l5").attr("class", "none")
				$("#atras").attr("style","display:block")
				console.log($pwidth)
		        break;

		    case 'l6':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab6").attr("class", "tab-pane") 
				$("#tab5").attr("class", "tab-pane active")
				$("#l5").attr("class", "active")
				$("#l6").attr("class", "none")
				$("#atras").attr("style","display:block")
				$("#siguiente").attr("style","display:block;float: right;")
				console.log($pwidth)
		        break;

			}
    });
    $('#atras2').on('click',function(e){
		var $pwidth=$('.active').attr("id");
			console.log($pwidth)
			switch ($pwidth) {
		    case 'l2':
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#form").attr("class", "alert alert-success display-none")
		    	$("#tab2").attr("class", "tab-pane")
				$("#tab1").attr("class", "tab-pane active")
				$("#l1").attr("class", "active")
				$("#l2").attr("class", "none")
				$("#atras").attr("style","display:none")
			console.log($pwidth)
		        break;

		    case 'l3':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#form").attr("class", "alert alert-success display-none")
		        $("#tab3").attr("class", "tab-pane") 
				$("#tab2").attr("class", "tab-pane active")
				$("#l2").attr("class", "active")
				$("#l3").attr("class", "none")
				$("#atras").attr("style","display:block")
				console.log($pwidth)
		        break;

		   case 'l4':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#form").attr("class", "alert alert-success display-none")
		        $("#tab4").attr("class", "tab-pane") 
				$("#tab3").attr("class", "tab-pane active")
				$("#l3").attr("class", "active")
				$("#l4").attr("class", "none")
				$("#atras").attr("style","display:block")
				console.log($pwidth)
		        break;

		    case 'l5':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#form").attr("class", "alert alert-success display-none")
		        $("#tab5").attr("class", "tab-pane") 
				$("#tab4").attr("class", "tab-pane active")
				$("#l4").attr("class", "active")
				$("#l5").attr("class", "none")
				$("#atras").attr("style","display:block")
				console.log($pwidth)
		        break;

		    case 'l6':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#form").attr("class", "alert alert-success display-none")
		        $("#tab6").attr("class", "tab-pane") 
				$("#tab5").attr("class", "tab-pane active")
				$("#l5").attr("class", "active")
				$("#l6").attr("class", "none")
				$("#atras").attr("style","display:block")
				$("#siguiente").attr("style","display:block;float: right;")
				console.log($pwidth)
		        break;

			}
    });

    $('#atras3').on('click',function(e){
		var $pwidth=$('.active').attr("id");
			console.log($pwidth)
			switch ($pwidth) {
		    case 'l2':
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		    	$("#tab2").attr("class", "tab-pane")
				$("#tab1").attr("class", "tab-pane active")
				$("#l1").attr("class", "active")
				$("#l2").attr("class", "none")
				$("#atras").attr("style","display:none")
				$("#evaluac").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
			console.log($pwidth)
		        break;

		    case 'l3':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab3").attr("class", "tab-pane") 
				$("#tab2").attr("class", "tab-pane active")
				$("#l2").attr("class", "active")
				$("#l3").attr("class", "none")
				$("#atras").attr("style","display:block")
				$("#evaluac").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
				console.log($pwidth)
		        break;

		   case 'l4':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab4").attr("class", "tab-pane") 
				$("#tab3").attr("class", "tab-pane active")
				$("#l3").attr("class", "active")
				$("#l4").attr("class", "none")
				$("#atras").attr("style","display:block")
				$("#evaluac").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
				console.log($pwidth)
		        break;

		    case 'l5':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab5").attr("class", "tab-pane") 
				$("#tab4").attr("class", "tab-pane active")
				$("#l4").attr("class", "active")
				$("#l5").attr("class", "none")
				$("#atras").attr("style","display:block")
				$("#evaluac").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
				console.log($pwidth)
		        break;

		    case 'l6':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab6").attr("class", "tab-pane") 
				$("#tab5").attr("class", "tab-pane active")
				$("#l5").attr("class", "active")
				$("#l6").attr("class", "none")
				$("#atras").attr("style","display:block")
				$("#siguiente").attr("style","display:block;float: right;")
				$("#evaluac").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
				console.log($pwidth)
		        break;

			}
    });

    $('#atras4').on('click',function(e){
		var $pwidth=$('.active').attr("id");
			console.log($pwidth)
			switch ($pwidth) {
		    case 'l2':
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		    	$("#tab2").attr("class", "tab-pane")
				$("#tab1").attr("class", "tab-pane active")
				$("#l1").attr("class", "active")
				$("#l2").attr("class", "none")
				$("#atras").attr("style","display:none")
			console.log($pwidth)
		        break;

		    case 'l3':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab3").attr("class", "tab-pane") 
				$("#tab2").attr("class", "tab-pane active")
				$("#l2").attr("class", "active")
				$("#l3").attr("class", "none")
				$("#atras").attr("style","display:block")
				console.log($pwidth)
		        break;

		   case 'l4':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab4").attr("class", "tab-pane") 
				$("#tab3").attr("class", "tab-pane active")
				$("#l3").attr("class", "active")
				$("#l4").attr("class", "none")
				$("#atras").attr("style","display:block")
				console.log($pwidth)
		        break;

		    case 'l5':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab5").attr("class", "tab-pane") 
				$("#tab4").attr("class", "tab-pane active")
				$("#l4").attr("class", "active")
				$("#l5").attr("class", "none")
				$("#atras").attr("style","display:block")
				console.log($pwidth)
		        break;

		    case 'l6':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab6").attr("class", "tab-pane") 
				$("#tab5").attr("class", "tab-pane active")
				$("#l5").attr("class", "active")
				$("#l6").attr("class", "none")
				$("#atras").attr("style","display:block")
				$("#siguiente").attr("style","display:block;float: right;")
				console.log($pwidth)
		        break;

			}
    });

    $('#atras5').on('click',function(e){
		var $pwidth=$('.active').attr("id");
			console.log($pwidth)
			switch ($pwidth) {
		    case 'l2':
		    	$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		    	$("#tab2").attr("class", "tab-pane")
				$("#tab1").attr("class", "tab-pane active")
				$("#l1").attr("class", "active")
				$("#l2").attr("class", "none")
				$("#atras").attr("style","display:none")
				$("#subido").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")


			console.log($pwidth)
		        break;

		    case 'l3':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab3").attr("class", "tab-pane") 
				$("#tab2").attr("class", "tab-pane active")
				$("#l2").attr("class", "active")
				$("#l3").attr("class", "none")
				$("#atras").attr("style","display:block")
				$("#subido").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
				console.log($pwidth)
		        break;

		   case 'l4':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab4").attr("class", "tab-pane") 
				$("#tab3").attr("class", "tab-pane active")
				$("#l3").attr("class", "active")
				$("#l4").attr("class", "none")
				$("#atras").attr("style","display:block")
				$("#subido").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
				console.log($pwidth)
		        break;

		    case 'l5':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab5").attr("class", "tab-pane") 
				$("#tab4").attr("class", "tab-pane active")
				$("#l4").attr("class", "active")
				$("#l5").attr("class", "none")
				$("#atras").attr("style","display:block")
				$("#subido").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
				console.log($pwidth)
		        break;

		    case 'l6':
		   		$("#error").attr("class", "alert alert-danger display-none")
			    $("#correcto").attr("class", "alert alert-success display-none")
		        $("#tab6").attr("class", "tab-pane") 
				$("#tab5").attr("class", "tab-pane active")
				$("#l5").attr("class", "active")
				$("#l6").attr("class", "none")
				$("#atras").attr("style","display:block")
				$("#siguiente").attr("style","display:block;float: right;")
				$("#subido").attr("style","display:none")
				$("#errorsubida").attr("style","display:none")
				console.log($pwidth)
		        break;

			}
    });



});
</script>

<!-- <script type="text/javascript">
    $(document).ready(function() {
        $.ajax({
                type: "POST",
                url: "getproveedor.php",
                success: function(response)
                {
                    $('.proveedor select').html(response).fadeIn();
                }
        });

    });
</script> -->
<script type="text/javascript">
    $(document).ready(function() {
        $.ajax({
                type: "POST",
                url: "getproveedor1.php",
                success: function(response)
                {
                    $('.proveedor1 select').html(response).fadeIn();
                }
        });

    });
</script>
<script type="text/javascript">
    $(document).ready(function() {
        $.ajax({
                type: "POST",
                url: "getproveedor2.php",
                success: function(response)
                {
                    $('.proveedor2 select').html(response).fadeIn();
                }
        });

    });
</script>
<script type="text/javascript">
    $(document).ready(function() {
        $.ajax({
                type: "POST",
                url: "getproveedor3.php",
                success: function(response)
                {
                    $('.proveedor3 select').html(response).fadeIn();
                }
        });

    });
</script>

<script type="text/javascript">
    $(document).ready(function() {
        $.ajax({
                type: "POST",
                url: "getproveedor4.php",
                success: function(response)
                {
                    $('.proveedor4 select').html(response).fadeIn();
                }
        });

    });
</script>
<script type="text/javascript">
    $(document).ready(function() {
        $.ajax({
                type: "POST",
                url: "getproveedor5.php",
                success: function(response)
                {
                    $('.proveedor5 select').html(response).fadeIn();
                }
        });

    });
</script>

 <script type="text/javascript">
        $(document).ready(function() {

            $('#btnAdd').click(function() {
                 var num     = $('.clonedInput').length;

                var newNum  = new Number(num + 1);

 
                var newElem = $('#input' + num).clone().attr('id', 'input' + newNum);
                var newElema = $('#out' + num).clone().attr('id','out' + newNum);

                newElem.children(':first').attr('id', 'name' + newNum).attr('name', 'name' + newNum).val('');
                newElema.children(':first').attr('id','ape' + newNum).attr('name','ape' + newNum).val('0');

                $('#input' + num).after(newElem);
                $('#out' + num).after(newElema);
                $("#btnDel").removeAttr("disabled");
 
                if (newNum == 10)
                    $('#btnAdd').attr('disabled','disabled');
               		 $("#btnDel").removeAttr("disabled");
            });
 
            $('#btnDel').click(function() {
                var num = $('.clonedInput').length;
 				console.log(num);
                $('#input' + num).remove();
                $('#out' + num).remove();
                $("#btnAdd").removeAttr("disabled");
 
                if (num-1 == 1){
                    $('#btnDel').attr('disabled','disabled');
                }
                
            });
            $("#btnDel").removeAttr("disabled");
        });
</script>

 <script type="text/javascript">
        $(document).ready(function() {
            $('#btnAdd1').click(function() {
                var num     = $('.clonedInput').length;

                var newNum  = new Number(num + 1);

 
                var newElem = $('#input' + num).clone().attr('id', 'input' + newNum);
                var newElema = $('#out' + num).clone().attr('id','out' + newNum);

                newElem.children(':first').attr('id', 'name' + newNum).attr('name', 'name' + newNum).val('');
                newElema.children(':first').attr('id','ape' + newNum).attr('name','ape' + newNum).val('0');

                $('#input' + num).after(newElem);
                $('#out' + num).after(newElema);
                $("#btnDel1").removeAttr("disabled");
 
                if (newNum == 10)
                    $('#btnAdd1').attr('disabled','disabled');
               		 $("#btnDel1").removeAttr("disabled");
            });
 
            $('#btnDel1').click(function() {
                var num = $('.clonedInput').length;
 				console.log(num);
                $('#input' + num).remove();
                $('#out' + num).remove();
                $("#btnAdd1").removeAttr("disabled");
 
                if (num-1 == 1){
                    $('#btnDel1').attr('disabled','disabled');
                }
                
            });
            $("#btnDel1").removeAttr("disabled");
        });
</script>

<script type="text/javascript">
        $(document).ready(function() {
            $('#btnAdda').click(function() {
                var num     = $('.clonedInput').length;

                var newNum  = new Number(num + 1);

 
                var newElem = $('#input' + num).clone().attr('id', 'input' + newNum);
                var newElema = $('#out' + num).clone().attr('id','out' + newNum);

                newElem.children(':first').attr('id', 'name' + newNum).attr('name', 'name' + newNum).val('');
                newElema.children(':first').attr('id','ape' + newNum).attr('name','ape' + newNum).val('0');

                $('#input' + num).after(newElem);
                $('#out' + num).after(newElema);
                $("#btnDela").removeAttr("disabled");
 
                if (newNum == 10)
                    $('#btnAdda').attr('disabled','disabled');
               		 $("#btnDela").removeAttr("disabled");
            });
 
            $('#btnDela').click(function() {
                var num = $('.clonedInput').length;
 				console.log(num);
                $('#input' + num).remove();
                $('#out' + num).remove();
                $("#btnAdda").removeAttr("disabled");
 
                if (num-1 == 1){
                    $('#btnDela').attr('disabled','disabled');
                }
                
            });
            $("#btnDela").removeAttr("disabled");
        });
</script>
<script type="text/javascript">
	function captar(){
		if (document.getElementById('psug').checked) {
			$("#pe").removeAttr('disabled');
			$("#ps").attr('disabled','disabled');

			$("#comentotro").removeAttr('readonly');
			$("#comentotro").attr('required','required');

			$("#pe").val("");
			var array = [];
			var elemen = "";
			if ($("#p1").val() != "") {
				//elemen .= '"'+$("p1").val()+'"';
				array.push($("#p1").val());
				if ($("#p2").val() != "") {
					//elemen .= ',"'+$("p2").val()+'"';
					array.push($("#p2").val());
					if ($("#p3").val() != "") {
						//elemen .= ',"'+$("p3").val()+'"';
						array.push($("#p3").val());
						if ($("#p4").val() != "") {
							//elemen .= ',"'+$("p4").val()+'"';
							array.push($("#p4").val());
							if ($("#p5").val() != "") {
								//elemen .= ',"'+$("p5").val()+'"';
								array.push($("#p5").val());
							}
						}
					}
				}
			}
			console.log(array);
		    var pe = document.getElementById("pe");
		    for(var i=0;i<array.length;i++){ 
		        pe.options[i] = new Option(array[i]);
		    }
		    $("#pelegido").val($("#pe").val());
		}
		else {
			$("#ps").removeAttr('disabled');
			$("#pe").attr('disabled','disabled');
			$("#pelegido").val($("#ps").val());
			$("#comentotro").removeAttr('required');
			$("#comentotro").attr('readonly','readonly');
			
		}
	}


</script>

 <script type="text/javascript">

$(document).ready(function(){
 
  var boton_rut;
  var boton_rut1;
  var boton_rut2;
  var boton_rut3;
  var boton_rut4;
  var cont;
  var eval;
  var constancia;
  var plaft;
  var sst;
  var cumpl;
  var homo;
  var contf;

  var fruc;
  var dnif;
  var consta;
  var vpoder;

  var seval;
  var sconstancia;
  var splaft;
  var ssst;
  var scumpl;
  var shomo;

  var doc_rut1;
  var doc_rut2;
  var doc_rut3;
  var doc_rut4;
  var doc_rut5;
  var doc_rut6;

  var sdoc_rut1;
  var sdoc_rut2;
  var sdoc_rut3;
  var sdoc_rut4;
  var sdoc_rut5;
  var sdoc_rut6;

  var pprov1;
  var pprov2;
  var pprov3;
  var pprov4;
  var pprov5;

  pprov1 = $('#ppro1');
  pprov2 = $('#ppro2');
  pprov3 = $('#ppro3');
  pprov4 = $('#ppro4');
  pprov5 = $('#ppro5');

  boton_rut = $('#cot');
  boton_rut1 = $('#cot1');
  boton_rut2 = $('#cot2');
  boton_rut3 = $('#cot3');
  boton_rut4 = $('#cot4');

  doc_rut1 = $('#doc1');
  doc_rut2 = $('#doc2');
  doc_rut3 = $('#doc3');
  doc_rut4 = $('#doc4');
  doc_rut5 = $('#doc5');
  doc_rut6 = $('#doc6');

  sdoc_rut1 = $('#sdoc1');
  sdoc_rut2 = $('#sdoc2');
  sdoc_rut3 = $('#sdoc3');
  sdoc_rut4 = $('#sdoc4');
  sdoc_rut5 = $('#sdoc5');
  sdoc_rut6 = $('#sdoc6');

  cont = $('#contrato1');
  fruc = $('#fruc');
  dnif = $('#dnif');
  consta = $('#cnadeudo');
  vpoder = $('#vpoder');

  contf = $('#contratofirmado');

  eval = $('#eval');
  constancia = $('#const');
  plaft = $('#plaft');
  sst = $('#sst');
  cumpl = $('#cumpl');
  homo = $('#homo');

  seval = $('#seval');
  sconstancia = $('#sconst');
  splaft = $('#splaft');
  ssst = $('#ssst');
  scumpl = $('#scumpl');
  shomo = $('#shomo');

  var minimo = 9999999999999999;

 pprov1.on('change', function(){
 	if (parseInt(pprov1.val()) > minimo) {
 		minimo = pprov1.val();

 		if (parseInt(pprov2.val()) < minimo && parseInt(pprov2.val()) > 0) {
 			minimo = parseInt(pprov2.val());
 		}
 		if (parseInt(pprov3.val()) < minimo && parseInt(pprov3.val()) > 0) {
 			minimo = parseInt(pprov3.val());
 		}
 		if (parseInt(pprov4.val()) < minimo && parseInt(pprov4.val()) > 0) {
 			minimo = parseInt(pprov4.val());
 		}
 		if (parseInt(pprov5.val()) < minimo && parseInt(pprov5.val()) > 0)  {
 			minimo = parseInt(pprov5.val());
 		}

 		$('#pminimo').val(minimo);
 	}
 	
 	if (parseInt(pprov1.val()) < minimo) {
 		minimo = parseInt(pprov1.val());
 		$('#pminimo').val(minimo);
 	}

 	if (parseInt(pprov1.val()) == 0) {
 		minimo = 99999999999;

 		if (parseInt(pprov2.val()) < minimo && parseInt(pprov2.val()) > 0) {
 			minimo = parseInt(pprov2.val());
 		}
 		if (parseInt(pprov3.val()) < minimo && parseInt(pprov3.val()) > 0) {
 			minimo = parseInt(pprov3.val());
 		}
 		if (parseInt(pprov4.val()) < minimo && parseInt(pprov4.val()) > 0) {
 			minimo = parseInt(pprov4.val());
 		}
 		if (parseInt(pprov5.val()) < minimo && parseInt(pprov5.val()) > 0)  {
 			minimo = parseInt(pprov5.val());
 		}
 		if (minimo == 99999999999 ) {
 			minimo = 0;
 		}

 		$('#pminimo').val(minimo);
 	}
    
  });

  pprov2.on('change', function(){
 	if (parseInt(pprov2.val()) > minimo) {
 		minimo = pprov2.val();
 		if (parseInt(pprov1.val()) < minimo && parseInt(pprov1.val()) > 0) {
 			minimo = parseInt(pprov1.val());
 		}
 		if (parseInt(pprov3.val()) < minimo && parseInt(pprov3.val()) > 0) {
 			minimo = parseInt(pprov3.val());
 		}
 		if (parseInt(pprov4.val()) < minimo && parseInt(pprov4.val()) > 0) {
 			minimo = parseInt(pprov4.val());
 		}
 		if (parseInt(pprov5.val()) < minimo && parseInt(pprov5.val()) > 0) {
 			minimo = parseInt(pprov5.val());
 		}
 		$('#pminimo').val(minimo);
 	}

 	if (parseInt(pprov2.val()) < minimo) {
 		minimo = parseInt(pprov2.val());
 		$('#pminimo').val(minimo);
 	}
    
     	if (parseInt(pprov2.val()) == 0) {
 		minimo = 99999999999;

 		if (parseInt(pprov1.val()) < minimo && parseInt(pprov1.val()) > 0) {
 			minimo = parseInt(pprov1.val());
 		}
 		if (parseInt(pprov3.val()) < minimo && parseInt(pprov3.val()) > 0) {
 			minimo = parseInt(pprov3.val());
 		}
 		if (parseInt(pprov4.val()) < minimo && parseInt(pprov4.val()) > 0) {
 			minimo = parseInt(pprov4.val());
 		}
 		if (parseInt(pprov5.val()) < minimo && parseInt(pprov5.val()) > 0)  {
 			minimo = parseInt(pprov5.val());
 		}
 		if (minimo == 99999999999 ) {
 			minimo = 0;
 		}

 		$('#pminimo').val(minimo);
 	}

  });
   pprov3.on('change', function(){
 	if (parseInt(pprov3.val()) > minimo ) {
 		minimo = pprov3.val();
 		if (parseInt(pprov2.val()) < minimo && parseInt(pprov2.val()) > 0) {
 			minimo = parseInt(pprov2.val());
 		}
 		if (parseInt(pprov1.val()) < minimo && parseInt(pprov1.val()) > 0) {
 			minimo = parseInt(pprov1.val());
 		}
 		if (parseInt(pprov4.val()) < minimo && parseInt(pprov4.val()) > 0) {
 			minimo = parseInt(pprov4.val());
 		}
 		if (parseInt(pprov5.val()) < minimo && parseInt(pprov5.val()) > 0) {
 			minimo = parseInt(pprov5.val());
 		}
 		$('#pminimo').val(minimo);
 	}

 	if (parseInt(pprov3.val()) < minimo) {
 		minimo = parseInt(pprov3.val());
 		$('#pminimo').val(minimo);
 	}
    
     	if (parseInt(pprov3.val()) == 0) {
 		minimo = 99999999999;

 		if (parseInt(pprov2.val()) < minimo && parseInt(pprov2.val()) > 0) {
 			minimo = parseInt(pprov2.val());
 		}
 		if (parseInt(pprov1.val()) < minimo && parseInt(pprov1.val()) > 0) {
 			minimo = parseInt(pprov1.val());
 		}
 		if (parseInt(pprov4.val()) < minimo && parseInt(pprov4.val()) > 0) {
 			minimo = parseInt(pprov4.val());
 		}
 		if (parseInt(pprov5.val()) < minimo && parseInt(pprov5.val()) > 0)  {
 			minimo = parseInt(pprov5.val());
 		}
 		if (minimo == 99999999999 ) {
 			minimo = 0;
 		}

 		$('#pminimo').val(minimo);
 	}

  });
    pprov4.on('change', function(){
 	if (parseInt(pprov4.val()) > minimo) {
 		minimo = pprov4.val();
 		if (parseInt(pprov2.val()) < minimo && parseInt(pprov2.val()) > 0) {
 			minimo = parseInt(pprov2.val());
 		}
 		if (parseInt(pprov3.val()) < minimo && parseInt(pprov3.val()) > 0) {
 			minimo = parseInt(pprov3.val());
 		}
 		if (parseInt(pprov1.val()) < minimo && parseInt(pprov1.val()) > 0) {
 			minimo = parseInt(pprov1.val());
 		}
 		if (parseInt(pprov5.val()) < minimo && parseInt(pprov5.val()) > 0) {
 			minimo = parseInt(pprov5.val());
 		}
 		$('#pminimo').val(minimo);
 	}

 	if (parseInt(pprov4.val()) < minimo) {
 		minimo = parseInt(pprov4.val());
 		$('#pminimo').val(minimo);
 	}
    
     	if (parseInt(pprov4.val()) == 0) {
 		minimo = 99999999999;

 		if (parseInt(pprov2.val()) < minimo && parseInt(pprov2.val()) > 0) {
 			minimo = parseInt(pprov2.val());
 		}
 		if (parseInt(pprov3.val()) < minimo && parseInt(pprov3.val()) > 0) {
 			minimo = parseInt(pprov3.val());
 		}
 		if (parseInt(pprov1.val()) < minimo && parseInt(pprov1.val()) > 0) {
 			minimo = parseInt(pprov1.val());
 		}
 		if (parseInt(pprov5.val()) < minimo && parseInt(pprov5.val()) > 0)  {
 			minimo = parseInt(pprov5.val());
 		}
 		if (minimo == 99999999999 ) {
 			minimo = 0;
 		}

 		$('#pminimo').val(minimo);
 	}

  });
     pprov5.on('change', function(){
 	if (parseInt(pprov5.val()) > minimo) {
 		minimo = pprov5.val();
 		if (parseInt(pprov2.val()) < minimo && parseInt(pprov2.val()) > 0) {
 			minimo = parseInt(pprov2.val());
 		}
 		if (parseInt(pprov3.val()) < minimo && parseInt(pprov3.val()) > 0) {
 			minimo = parseInt(pprov3.val());
 		}
 		if (parseInt(pprov4.val()) < minimo && parseInt(pprov4.val()) > 0) {
 			minimo = parseInt(pprov4.val());
 		}
 		if (parseInt(pprov1.val()) < minimo && parseInt(pprov1.val()) > 0) {
 			minimo = parseInt(pprov1.val());
 		}
 		$('#pminimo').val(minimo);
 	}

 	if (parseInt(pprov5.val()) < minimo) {
 		minimo = parseInt(pprov5.val());
 		$('#pminimo').val(minimo);
 	}
    
     	if (parseInt(pprov5.val()) == 0) {
 		minimo = 99999999999;

 		if (parseInt(pprov2.val()) < minimo && parseInt(pprov2.val()) > 0) {
 			minimo = parseInt(pprov2.val());
 		}
 		if (parseInt(pprov3.val()) < minimo && parseInt(pprov3.val()) > 0) {
 			minimo = parseInt(pprov3.val());
 		}
 		if (parseInt(pprov4.val()) < minimo && parseInt(pprov4.val()) > 0) {
 			minimo = parseInt(pprov4.val());
 		}
 		if (parseInt(pprov1.val()) < minimo && parseInt(pprov1.val()) > 0)  {
 			minimo = parseInt(pprov1.val());
 		}
 		if (minimo == 99999999999 ) {
 			minimo = 0;
 		}

 		$('#pminimo').val(minimo);
 	}
  });

  fruc.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#fruc');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#dfruc").val("")
      $("#estadofruc").html("Sin Documento");
      $('#estadofruc').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#dfruc").val(valor_rut);
       $("#estadofruc").html("Con Documento");
       $('#estadofruc').attr("class","btn btn-lg green");
    }
    
  });

  dnif.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#dnif');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#ddnif").val("")
    	console.log("#ddnif");
      $("#estadodnif").html("Sin Documento");
      $('#estadodnif').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#ddnif").val(valor_rut);
    	console.log("#ddnif");
       $("#estadodnif").html("Con Documento");
       $('#estadodnif').attr("class","btn btn-lg green");
    }
    
  });

  consta.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#cnadeudo');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#dcnadeudo").val("")
      $("#estadocnadeudo").html("Sin Documento");
      $('#estadocnadeudo').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#dcnadeudo").val(valor_rut);
       $("#estadocnadeudo").html("Con Documento");
       $('#estadocnadeudo').attr("class","btn btn-lg green");
    }
    
  });

  vpoder.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#vpoder');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#dvpoder").val("")
      $("#estadovpoder").html("Sin Documento");
      $('#estadovpoder').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#dvpoder").val(valor_rut);
       $("#estadovpoder").html("Con Documento");
       $('#estadovpoder').attr("class","btn btn-lg green");
    }
    
  });

  seval.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#seval');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#sdoc1").val("")
      $("#sestadob1").html("Sin Sustento");
      $('#sestadob1').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#sdoc1").val(valor_rut);
       $("#sestadob1").html("Con Sustento");
       $('#sestadob1').attr("class","btn btn-lg green");
    }
    
  });

  sconstancia.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#sconst');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#sdoc2").val("")
      $("#sestadob2").html("Sin Sustento");
      $('#sestadob2').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#sdoc2").val(valor_rut);
       $("#sestadob2").html("Con Sustento");
       $('#sestadob2').attr("class","btn btn-lg green");
    }
    
  });

  splaft.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#splaft');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#sdoc3").val("")
      $("#sestadob3").html("Sin Sustento");
      $('#sestadob3').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#sdoc3").val(valor_rut);
       $("#sestadob3").html("Con Sustento");
       $('#sestadob3').attr("class","btn btn-lg green");
    }
    
  });

  ssst.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#ssst');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#sdoc4").val("")
      $("#sestadob4").html("Sin Sustento");
      $('#sestadob4').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#sdoc4").val(valor_rut);
       $("#sestadob4").html("Con Sustento");
       $('#sestadob4').attr("class","btn btn-lg green");
    }
    
  });

  scumpl.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#scumpl');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#sdoc5").val("")
      $("#sestadob5").html("Sin Sustento");
      $('#sestadob5').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#sdoc5").val(valor_rut);
       $("#sestadob5").html("Con Sustento");
       $('#sestadob5').attr("class","btn btn-lg green");
    }
    
  });

  shomo.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#shomo');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#sdoc6").val("")
      $("#sestadob6").html("Sin Sustento");
      $('#sestadob6').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#sdoc6").val(valor_rut);
       $("#sestadob6").html("Con Sustento");
       $('#sestadob6').attr("class","btn btn-lg green");
    }
    
  });


  eval.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#eval');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#doc1").val("")
      $("#estadob1").html("Sin Documento");
      $('#estadob1').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#doc1").val(valor_rut);
       $("#estadob1").html("Con Documento");
       $('#estadob1').attr("class","btn btn-lg green");
    }
    
  });

  constancia.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#const');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#doc2").val("")
      $("#estadob2").html("Sin Documento");
      $('#estadob2').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#doc2").val(valor_rut);
       $("#estadob2").html("Con Documento");
       $('#estadob2').attr("class","btn btn-lg green");
    }
    
  });

  plaft.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#plaft');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#doc3").val("")
      $("#estadob3").html("Sin Documento");
      $('#estadob3').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#doc3").val(valor_rut);
       $("#estadob3").html("Con Documento");
       $('#estadob3').attr("class","btn btn-lg green");
    }
    
  });

  sst.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#sst');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#doc4").val("")
      $("#estadob4").html("Sin Documento");
      $('#estadob4').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#doc4").val(valor_rut);
       $("#estadob4").html("Con Documento");
       $('#estadob4').attr("class","btn btn-lg green");
    }
    
  });

  cumpl.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#cumpl');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#doc5").val("")
      $("#estadob5").html("Sin Documento");
      $('#estadob5').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#doc5").val(valor_rut);
       $("#estadob5").html("Con Documento");
       $('#estadob5').attr("class","btn btn-lg green");
    }
    
  });

  homo.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#homo');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#doc6").val("")
      $("#estadob6").html("Sin Documento");
      $('#estadob6').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#doc6").val(valor_rut);
       $("#estadob6").html("Con Documento");
       $('#estadob6').attr("class","btn btn-lg green");
    }
    
  });

  cont.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#contrato1');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
      $("#contra").val("")
      $("#estadob").html("Sin Documento");
      $('#estadob').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#contra").val(valor_rut);
       $("#estadob").html("Con Documento");
       $('#estadob').attr("class","btn btn-lg green");
    }
    
  });

    contf.on('change', function(){
    var valor_input, valor_rut;
    
    valor_input = $('#contratofirmado');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
      $("#dcontratofirmado").val("");
      $("#estadof").html("Sin Documento");
      $('#estadof').attr("class","btn btn-lg grey-cascade");
    }else{
    	$("#dcontratofirmado").val(valor_rut);
       $("#estadof").html("Con Documento");
       $('#estadof').attr("class","btn btn-lg green");
    }
    
  });
  
  boton_rut.on('change', function(){
    
    var valor_input, valor_rut;
    
    valor_input = $('#cot');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
    	$("#cote").val("");
      $("#control").attr("class", "fa fa-file");

    }else{
       $("#cote").val(valor_rut);
       $("#control").attr("class", "fa fa-check");
    }
    
  }); 
   boton_rut1.on('change', function(){
    
    var valor_input, valor_rut;
    
    valor_input = $('#cot1');
    valor_rut = valor_input.val();

    if(valor_rut === ''){
    	$("#cote1").val("");
    	$("#pelegido").val($("#ps").val());
	   $("#control1").attr("class", "fa fa-file");
    }else{
    	$("#cote1").val(valor_rut);
       $("#control1").attr("class", "fa fa-check");
    }
    
  });
    boton_rut2.on('change', function(){
    
    var valor_input, valor_rut;
    
    valor_input = $('#cot2');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
      $("#cote2").val("");
      $("#control2").attr("class", "fa fa-file");

    }else{
       $("#cote2").val(valor_rut);
       $("#control2").attr("class", "fa fa-check");
    }
    
  });
     boton_rut3.on('change', function(){
    
    var valor_input, valor_rut;
    
    valor_input = $('#cot3');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
      $("#cote3").val("");
      $("#control3").attr("class", "fa fa-file");

    }else{
       $("#cote3").val(valor_rut);
       $("#control3").attr("class", "fa fa-check");
    }
    
  });
      boton_rut4.on('change', function(){
    
    var valor_input, valor_rut;
    
    valor_input = $('#cot4');
    valor_rut = valor_input.val();
    
    if(valor_rut === ''){
      $("#cote4").val("");
      $("#control4").attr("class", "fa fa-file");

    }else{
       $("#cote4").val(valor_rut);	
       $("#control4").attr("class", "fa fa-check");
    }
    
  });
  
});
</script>

<script>
jQuery(document).ready(function() {       
   UIToastr.init();
});
</script>

<script type="text/javascript">
	$(document).on('input', '.inputs', function(){
	$("#pesos").val("0");
    var add = 0;
		$(".inputs").each(function() {
		add += Number($(this).val());
		});
		$("#pesos").val(add);
	});

	$(document).on('input', '#pe', function(){
	$("#pelegido").val($("#pe").val());
	});

		$(document).on('input', '.legal', function(){
    var add = 0;
		$(".legal").each(function() {
			if ($(this).val() != "") {
				add += 1;
			}else{
				add += 0;
			}
		});
		$("#resultadosestado").val("Se completaron " + add + " de 15 campos");
	});
</script>


<script type="text/javascript">
	function total(){
	var re;
    var valor = 0
    var valor1 = 0
    var valor2 = 0
    var valor3 = 0
    var valor4 = 0
    $('.stotal').each(function(){
        re = $(this).val();
        valor += parseFloat(re)
    });
    if(valor=="100"){
	$('#total').html("0.00");
    }else{
    	console.log($('#total').val());
    $('#total').html(valor.toFixed(2));
	}

     $('.stotal1').each(function(){
        re = $(this).val();
        valor1 += parseFloat(re)
    });
     if (valor1=="100") {
     $('#total1').html("0.00");
     }else{
    $('#total1').html(valor1.toFixed(2));
	}

     $('.stotal2').each(function(){
        re = $(this).val();
  
        valor2 += parseFloat(re)
    });
     if(valor2=="100"){
     $('#total2').html("0.00");
     }else{
    $('#total2').html(valor2.toFixed(2));
    }

     $('.stotal3').each(function(){
        re = $(this).val();
    
        valor3 += parseFloat(re)
    });
     if (valor3=="100") {
     $('#total3').html("0.00");	
     }
     else{
    $('#total3').html(valor3.toFixed(2));
	}

     $('.stotal4').each(function(){
        re = $(this).val();
     
        valor4 += parseFloat(re)
    });
     if (valor4=="100") {
     $('#total4').html("0.00");

     }else{
    $('#total4').html(valor4.toFixed(2));
	}
	elegido();
	};
</script>
<script type="text/javascript">
	function elegido(){
		console.log("evaluado");
		console.log($('#total').html());
		console.log($('#total1').html());
		console.log($('#total2').html());
		console.log($('#total3').html());
		console.log($('#total4').html());

		if (parseFloat($('#total').html())>parseFloat($('#total1').html())) {
				if(parseFloat($('#total').html())>parseFloat($('#total2').html())){
					if(parseFloat($('#total').html())>parseFloat($('#total3').html())){
						if(parseFloat($('#total').html())>parseFloat($('#total4').html())){
							$('#ps').val($('#p1').val());
							$("#pelegido").val($("#ps").val());

							$('#total').attr("style","left:42%; color: red; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total1').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total2').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total3').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total4').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");

						}else{
							$('#ps').val($('#p5').val());
							$("#pelegido").val($("#ps").val());

							$('#total').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total1').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total2').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total3').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total4').attr("style","left:42%; color: red; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");

						}
					}else{
						if(parseFloat($('#total3').html())>parseFloat($('#total4').html())){
							$('#ps').val($('#p4').val());
							$("#pelegido").val($("#ps").val());

							$('#total').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total1').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total2').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total3').attr("style","left:42%; color: red; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total4').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");

						}else{
							$('#ps').val($('#p5').val());
							$("#pelegido").val($("#ps").val());

							$('#total').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total1').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total2').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total3').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total4').attr("style","left:42%; color: red; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");

						}
					}
				}else{
					if(parseFloat($('#total2').html())>parseFloat($('#total3').html())){
						if(parseFloat($('#total2').html())>parseFloat($('#total4').html())){
							$('#ps').val($('#p3').val());
							$("#pelegido").val($("#ps").val());

							$('#total').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total1').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total2').attr("style","left:42%; color: red; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total3').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total4').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");

						}else{
							$('#ps').val($('#p5').val());
							$("#pelegido").val($("#ps").val());

							$('#total').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total1').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total2').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total3').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total4').attr("style","left:42%; color: red; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");

						}
					}else{
						if(parseFloat($('#total3').html())>parseFloat($('#total4').html())){
							$('#ps').val($('#p4').val());
							$("#pelegido").val($("#ps").val());

							$('#total').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total1').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total2').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total3').attr("style","left:42%; color: red; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total4').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");

						}else{
							$('#ps').val($('#p5').val());
							$("#pelegido").val($("#ps").val());

							$('#total').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total1').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total2').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total3').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total4').attr("style","left:42%; color: red; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");

						}
					}
				}
		}else{
			if(parseFloat($('#total1').html())>parseFloat($('#total2').html())){
					if(parseFloat($('#total1').html())>parseFloat($('#total3').html())){
						if(parseFloat($('#total1').html())>parseFloat($('#total4').html())){
							$('#ps').val($('#p2').val());
							$("#pelegido").val($("#ps").val());

							$('#total').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total1').attr("style","left:42%; color: red; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total2').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total3').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total4').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");

						}else{
							$('#ps').val($('#p5').val());
							$("#pelegido").val($("#ps").val());

							$('#total').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total1').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total2').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total3').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total4').attr("style","left:42%; color: red; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");

						}
					}else{
						if(parseFloat($('#total3').html())>parseFloat($('#total4').html())){
							$('#ps').val($('#p4').val());
							$("#pelegido").val($("#ps").val());

							$('#total').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total1').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total2').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total3').attr("style","left:42%; color: red; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total4').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");

						}else{
							$('#ps').val($('#p5').val());
							$("#pelegido").val($("#ps").val());

							$('#total').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total1').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total2').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total3').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total4').attr("style","left:42%; color: red; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");

						}
					}
				}else{
					if(parseFloat($('#total2').html())>parseFloat($('#total3').html())){
						if(parseFloat($('#total2').html())>parseFloat($('#total4').html())){
							$('#ps').val($('#p3').val());
							$("#pelegido").val($("#ps").val());

							$('#total').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total1').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total2').attr("style","left:42%; color: red; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total3').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total4').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");

						}else{
							$('#ps').val($('#p5').val());
							$("#pelegido").val($("#ps").val());

							$('#total').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total1').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total2').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total3').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total4').attr("style","left:42%; color: red; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");

						}
					}else{
						if(parseFloat($('#total3').html())>parseFloat($('#total4').html())){
							$('#ps').val($('#p4').val());
							$("#pelegido").val($("#ps").val());

							$('#total').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total1').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total2').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total3').attr("style","left:42%; color: red; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total4').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");

						}else{
							$('#ps').val($('#p5').val());
							$("#pelegido").val($("#ps").val());

							$('#total').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total1').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total2').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total3').attr("style","left:42%; color: gray; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");
							$('#total4').attr("style","left:42%; color: red; width: 50px; height: 30px;text-align: center;border:none;padding-top: 7px;");

						}
					}
				}
		}
	}
</script>

<script type="text/javascript">
	$(document).on('input', '#p1', function(){
    $("#idp").val($('#p1').val());
    $("#idp").attr('selected','selected');
    $('#evaluador').html("EVALUAR");
    $('#ps').val("");
    $('#evaluador').attr("class","btn yellow");
	});

	$(document).on('input', '#p2', function(){
    $("#idp").val($('#p2').val());
    $('#evaluador1').html("EVALUAR");
     $('#ps').val("");
    $('#evaluador1').attr("class","btn yellow");
	});

	$(document).on('input', '#p3', function(){
    $("#idp").val($('#p3').val());
    $('#evaluador2').html("EVALUAR");
     $('#ps').val("");
    $('#evaluador2').attr("class","btn yellow");
	});

	$(document).on('input', '#p4', function(){
    $("#idp").val($('#p4').val());
    $('#evaluador3').html("EVALUAR");
     $('#ps').val("");
    $('#evaluador3').attr("class","btn yellow");
	});

	$(document).on('input', '#p5', function(){
    $("#idp").val($('#p5').val());
    $('#evaluador4').html("EVALUAR");
     $('#ps').val("");
    $('#evaluador4').attr("class","btn yellow");
	});
</script>
<script type="text/javascript">
	$('#evaluador').on('click',function(){
	$("#tmp").val($('#evaluador').attr("id"));
	$("#idp").val($('#p1').val());
	console.log($('#idp').val());
	$("#tprov").val("1");
	});

	$('#evaluador1').on('click',function(){
	$("#tmp").val($('#evaluador1').attr("id"));

	$("#idp").val($('#p2').val());
	console.log($('#idp').val());
	$("#tprov").val("2");
	});

	$('#evaluador2').on('click',function(){
	$("#tmp").val($('#evaluador2').attr("id"));

	$("#idp").val($('#p3').val());
	console.log($('#idp').val());
	$("#tprov").val("3");
	});

	$('#evaluador3').on('click',function(){
	$("#tmp").val($('#evaluador3').attr("id"));

	$("#idp").val($('#p4').val());
	console.log($('#idp').val());
	$("#tprov").val("4");
	});

	$('#evaluador4').on('click',function(){
	$("#tmp").val($('#evaluador4').attr("id"));

	$("#idp").val($('#p5').val());
	console.log($('#idp').val());
	$("#tprov").val("5");
	});
</script>

<script type="text/javascript">
  $(document).on('click', '#evaluador', function(){
  //$('#dataModal').modal();
  var idp = "1";
   $.ajax({
   url:"selectval.php",
   method:"POST",
   data:{idp:idp},
   success:function(data){
    $('#valorado').html(data);
    $('#valor').modal('show');
   }
   });
  });
  $(document).on('click', '#evaluador1', function(){
  //$('#dataModal').modal();
  var idp = "2";
   $.ajax({
   url:"selectval.php",
   method:"POST",
   data:{idp:idp},
   success:function(data){
    $('#valorado').html(data);
    $('#valor').modal('show');
   }
   });
  });
  $(document).on('click', '#evaluador2', function(){
  //$('#dataModal').modal();
  var idp = "3";
   $.ajax({
   url:"selectval.php",
   method:"POST",
   data:{idp:idp},
   success:function(data){
    $('#valorado').html(data);
    $('#valor').modal('show');
   }
   });
  });
  $(document).on('click', '#evaluador3', function(){
  //$('#dataModal').modal();
  var idp = "4";
   $.ajax({
   url:"selectval.php",
   method:"POST",
   data:{idp:idp},
   success:function(data){
    $('#valorado').html(data);
    $('#valor').modal('show');
   }
   });
  });
  $(document).on('click', '#evaluador4', function(){
  //$('#dataModal').modal();
  var idp = "5";
   $.ajax({
   url:"selectval.php",
   method:"POST",
   data:{idp:idp},
   success:function(data){
    $('#valorado').html(data);
    $('#valor').modal('show');
   }
   });
  });



  $(document).on('click', '#resumido', function(){
  //$('#dataModal').modal();
  var idp = "1";
   $.ajax({
   url:"selectresumen.php",
   method:"POST",
   data:{idp:idp},
   success:function(data){
    $('#resumentab').html(data);
    $('#resumentablero').modal('show');
   }
   });
  });

    $(document).on('click', '#clausulas', function(){
  //$('#dataModal').modal();
   $.ajax({
   url:"selectclausula.php",
   method:"POST",
   success:function(data){
    $('#clausulatab').html(data);
    $('#clausulatablero').modal('show');
   }
   });
  });

  $(document).on('click', '#evaluacion', function(){
  //$('#dataModal').modal();
  var idp = "1";
   $.ajax({
   url:"selectval1.php",
   method:"POST",
   data:{idp:idp},
   success:function(data){
    $('#valorado1').html(data);
    $('#valor1').modal('show');
   }
   });
  });

  $(document).on('click', '#evaluacion1', function(){
  //$('#dataModal').modal();
  var idp = "2";
   $.ajax({
   url:"selectval1.php",
   method:"POST",
   data:{idp:idp},
   success:function(data){
    $('#valorado1').html(data);
    $('#valor1').modal('show');
   }
   });
  });
  $(document).on('click', '#evaluacion2', function(){
  //$('#dataModal').modal();
  var idp = "3";
   $.ajax({
   url:"selectval1.php",
   method:"POST",
   data:{idp:idp},
   success:function(data){
    $('#valorado1').html(data);
    $('#valor1').modal('show');
   }
   });
  });
  $(document).on('click', '#evaluacion3', function(){
  //$('#dataModal').modal();
  var idp = "4";
   $.ajax({
   url:"selectval1.php",
   method:"POST",
   data:{idp:idp},
   success:function(data){
    $('#valorado1').html(data);
    $('#valor1').modal('show');
   }
   });
  });
  $(document).on('click', '#evaluacion4', function(){
  //$('#dataModal').modal();
  var idp = "5";
   $.ajax({
   url:"selectval1.php",
   method:"POST",
   data:{idp:idp},
   success:function(data){
    $('#valorado1').html(data);
    $('#valor1').modal('show');
   }
   });
  });



  //$('#dataModal').modal();
  function completar(){
  var idp = "enviado";
   $.ajax({
   url:"selectval2.php",
   method:"POST",
   data:{idp:idp},
   success:function(data){
    $('#operaciones').html(data);
    total();
    }
   });
  };

</script>

</body>
</html>
