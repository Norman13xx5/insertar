# Conexion

<?php
function conectar()
{
    $host = "localhost";
    $user = "root";
    $pass = "";
    $bd = "crud2";
    $conn = mysqli_connect($host, $user, $pass, $bd);
    mysqli_select_db($conn, $bd);
    return $conn;
}



------------------------------------------------------------------------------------------------------------------------------------------------------------
#Validar login

<?php
include("../conexion.php");
$conn = conectar();

$usuario = $_POST['username'];
$password = $_POST['password'];
session_start();
$_SESSION['usuario'] = $usuario;

$sql = "SELECT*FROM usuario WHERE user='$usuario' and contraseña='$password' ";
$query = mysqli_query($conn, $sql);

if (mysqli_num_rows($query) >= 1) {

    $filas = mysqli_fetch_array($query);

    if ($filas['id_cargo'] == 1) { //administrador
        header("location:../../template/views/admin.php");
    } elseif ($filas['id_cargo'] == 2) {
        header("location:../../template/views/cliente.php");
    }
} else {
    echo '<script type="text/javascript">
    alert("Usuario o contraseña incorrecto!");
    window.location.href="../../login.php"; 
    </script>';
}

mysqli_close($conn);



------------------------------------------------------------------------------------------------------------------------------------------------------------
#html para insertar


<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
    <title>Insertar Datos</title>
</head>
<body>
    <div class="container mt-5">
        <div class="row">

            <form action="../../config/functions/insertar.php" method="POST">
                <div class="mb-3 mt-3">
                    <label for="placa" class="form-label">Placa:</label>
                    <input type="hidden" class="form-control" id="id" name="id">
                    <input type="text" class="form-control" id="placa" placeholder="Ingrese Placa" name="placa">
                </div>
                <div class="mb-3 mt-3">
                    <label for="marca_modelo" class="form-label">Marca/Modelo:</label>
                    <input type="text" class="form-control" id="marca_modelo" placeholder="Ingrese Marca/Modelo" name="marca_modelo">
                </div>
                <div class="mb-3 mt-3">
                    <label for="fecha_ingreso" class="form-label">Fecha Ingreso:</label>
                    <input type="date" class="form-control" id="fecha_ingreso" placeholder="Ingrese Fecha Ingreso" name="fecha_ingreso">
                </div>
                <div class="form-check mb-3">
                    <label class="form-check-label">
                    </label>
                </div>
                <input type="submit" class="btn btn-primary">
            </form>

        </div>
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.2/dist/umd/popper.min.js" integrity="sha384-IQsoLXl5PILFhosVNubq5LC7Qb9DXgDA9i+tQ8Zj3iwWAwPtgFTxbJ8NT4GN1R8p" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.min.js" integrity="sha384-cVKIPhGWiC2Al4u+LWgxfKTRIcfu0JTxR+EQDz/bgldoEyl4H0zUF0QKbrJ0EcQF" crossorigin="anonymous"></script>
</html>


---------------------------------------------
# insertar


<?php
include("../conexion.php");
$conn = conectar();

$placa = $_POST['placa'];
$marca_modelo = $_POST['marca_modelo'];
$fecha_ingreso = $_POST['fecha_ingreso'];

$sql = "INSERT INTO `vehiculo_taller` (`placa`, `marca_modelo`, `fecha_ingreso`) VALUES ('$placa', '$marca_modelo', '$fecha_ingreso') ";
$query = mysqli_query($conn, $sql);

if($query){
    header("location:../../template/views/admin.php");
}else{
    echo '<script type="text/javascript">
    alert("No se ha podido insertar correctamente");
    window.location.href="../../template/views/admin.php"; 
    </script>';
}


------------------------------------------------------------------------------------------------------------------------------------------------------------



#HTML PARA PINTAR JUNTO CON EL INSERTAR


<?php
include("../../config/conexion.php");
$conn = conectar();

$sql = "SELECT * FROM `vehiculo_taller` ";
$query = mysqli_query($conn, $sql);

?>
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
    <title>Insertar Datos</title>
</head>
<body>
    <div class="container mt-5">
        <div class="row">
          
            <form action="../../config/functions/insertar.php" method="POST">
                <div class="mb-3 mt-3">
                    <label for="placa" class="form-label">Placa:</label>
                    <input type="hidden" class="form-control" id="id" name="id">
                    <input type="text" class="form-control" id="placa" placeholder="Ingrese Placa" name="placa">
                </div>
                <div class="mb-3 mt-3">
                    <label for="marca_modelo" class="form-label">Marca/Modelo:</label>
                    <input type="text" class="form-control" id="marca_modelo" placeholder="Ingrese Marca/Modelo" name="marca_modelo">
                </div>
                <div class="mb-3 mt-3">
                    <label for="fecha_ingreso" class="form-label">Fecha Ingreso:</label>
                    <input type="date" class="form-control" id="fecha_ingreso" placeholder="Ingrese Fecha Ingreso" name="fecha_ingreso">
                </div>
                <div class="form-check mb-3">
                    <label class="form-check-label">
                    </label>
                </div>
                <input type="submit" class="btn btn-primary">
            </form>


            <div class="container mt-3">
                <h2>Datos</h2>
                <table class="table">
                    <thead>
                        <tr>
                            <th>Id</th>
                            <th>Placa</th>
                            <th>Marca/Modelo</th>
                            <th>Fecha Ingreso</th>
                            <th></th>
                            <th></th>
                        </tr>
                    </thead>
                    <tbody>
                        <?php
                        while ($row = mysqli_fetch_array($query)) {
                        ?>
                            <tr>
                                <th><?php echo $row['id'] ?></th>
                                <th><?php echo $row['placa'] ?></th>
                                <th><?php echo $row['marca_modelo'] ?></th>
                                <th><?php echo $row['fecha_ingreso'] ?></th>
                                <th><a href="../../config/functions/actualizar.php?id=<?php echo $row['id'] ?>" class="btn btn-info">Editar</a></th>
                                <th><a href="../../config/functions/eliminar.php?id=<?php echo $row['id'] ?>" class="btn btn-danger">Eliminar</a></th>
                            </tr>
                        <?php
                        }
                        ?>
                    </tbody>
                </table>
            </div>

        </div>
    </div>
</body>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.2/dist/umd/popper.min.js" integrity="sha384-IQsoLXl5PILFhosVNubq5LC7Qb9DXgDA9i+tQ8Zj3iwWAwPtgFTxbJ8NT4GN1R8p" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.min.js" integrity="sha384-cVKIPhGWiC2Al4u+LWgxfKTRIcfu0JTxR+EQDz/bgldoEyl4H0zUF0QKbrJ0EcQF" crossorigin="anonymous"></script>
</html>



------------------------------------------------------------------------------------------------------------------------------------------------------------


# Eliminar


<?php
include("../conexion.php");
$conn = conectar();

$id = $_GET['id'];

$sql = "DELETE FROM cliente WHERE id = '$id' ";
$query = mysqli_query($conn, $sql);

if ($query) {
    header("location:../../template/views/admin.php");
} else {
    echo '<script type="text/javascript">
    alert("No se pudo eliminar correctamente");
    window.location.href="../../template/views/admin.php"; 
    </script>';
}

------------------------------------------------------------------------------------------------------------------------------------------------------------


#HTML PARA ACTUALIZAR


<?php
include("../conexion.php");
$conn = conectar();

$id = $_GET['id'];

$sql = "SELECT * FROM cliente WHERE id='$id' ";
$query = mysqli_query($conn,$sql);

$row = mysqli_fetch_array($query);

?>

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
    <title>Document</title>
</head>
<body>
    <div class="container mt-5">
        <div class="row">
          
            <form action="update.php" method="POST">
                    <input type="hidden" class="form-control" id="id" name="id" value="<?php echo $row['id'] ?>">
                <div class="mb-3 mt-3">
                    <label for="cedula" class="form-label">Cedula:</label>
                    <input type="int" class="form-control" id="cedula" placeholder="Ingrese cedula" name="cedula" value="<?php echo $row['cedula'] ?>">
                </div>
                <div class="mb-3 mt-3">
                    <label for="nombre" class="form-label">Nombre:</label>
                    <input type="int" class="form-control" id="nombre" placeholder="Ingrese nombre" name="nombre" value="<?php echo $row['nombre'] ?>">
                </div>
                <div class="mb-3 mt-3">
                    <label for="apeliido" class="form-label">Apellido:</label>
                    <input type="int" class="form-control" id="apellido" placeholder="Ingrese apellido" name="apellido" value="<?php echo $row['apellido'] ?>">
                </div>
                <div class="form-check mb-3">
                    <label class="form-check-label">
                    </label>
                </div>
                <input type="submit" class="btn btn-primary">
            </form>
        </div>
    </div>

</body>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.2/dist/umd/popper.min.js" integrity="sha384-IQsoLXl5PILFhosVNubq5LC7Qb9DXgDA9i+tQ8Zj3iwWAwPtgFTxbJ8NT4GN1R8p" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.min.js" integrity="sha384-cVKIPhGWiC2Al4u+LWgxfKTRIcfu0JTxR+EQDz/bgldoEyl4H0zUF0QKbrJ0EcQF" crossorigin="anonymous"></script>
</html>


------------------------------------------------------------------------------------------------------------------------------------------------------------

#UPDATE


<?php
include("../conexion.php");
$conn = conectar();

$id = $_POST['id'];
$cedula = $_POST['cedula'];
$nombre = $_POST['nombre'];
$apellido = $_POST['apellido'];

$sql = "UPDATE `cliente` SET `cedula` = '$cedula', `nombre` = '$nombre', `apellido` = '$apellido' WHERE `id` = '$id' ";
$query = mysqli_query($conn, $sql);

if ($query) {
    header("location:../../template/views/admin.php");
} else {
    echo '<script type="text/javascript">
    alert("No se pudo actualizar correctamente");
    window.location.href="../../template/views/admin.php"; 
    </script>';
}

















