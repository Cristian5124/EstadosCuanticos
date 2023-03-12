<h1 align="center">ESTADOS CUÁNTICOS</h1>
<img src="https://universitam.com/academicos/wp-content/uploads/2016/04/crop.png" alt="" class="Complex" width=100%>

`Esta librería contiene funciones en Python que logran simular algunos de los experimentos más conocidos en la computación cuántica.` <br>
`Algunos de los aspectos más relevantes de este trabajo son:` <br><br>
✔️ Comentarios en todas las operaciones matemáticas para una lectura más sencilla. <br>
✔️ Funciones individuales que simulan experimentos diferentes en el lenguaje de programación. <br>
✔️ Graficación de un diagrama de barras que permite visualizar las probabilidades de un vector de estados.
<hr>

<h2 align="left">Código Fuente</h2>

    import numpy as np
    import matplotlib.pyplot as plt

    def canicas(coefbooleanos, estinicial):

        # Dimensión de la matriz
        n = len(coefbooleanos)

        # Verificación para saber si la matriz es cuadrada
        for fila in coefbooleanos:
            if len(fila) != n:
                print("La matriz no es cuadrada.")

        # Verificación para saber si el estado inicial tiene el mismo tamaño que la matriz
        if len(estinicial) != n:
            print("El estado inicial no tiene el mismo tamaño que la matriz.")

        # Cálculo del estado final de las canicas
        estfinal = [False] * n
        for j in range(n):
            for i in range(n):
                if coefbooleanos[i][j]:
                    estfinal[j] = estfinal[j] or estinicial[i]

        return estfinal

    def multrendijasclasico(nrendijas, ndetectores, probrendijas):

        # Creación de la matriz
        matriz = np.zeros((ndetectores, ndetectores))

        # Multiplicación de las matrices de probabilidad para obtener la matriz de transición
        for i in range(ndetectores):
            for j in range(nrendijas):
                for k in range(ndetectores):
                    matriz[i][k] += probrendijas[j][i] * probrendijas[j][k]

        # Vector ket
        ket = np.zeros((ndetectores,1))
        ket[0] = 1

        # Probabilidades
        ketfinal = np.dot(matriz, ket)
        probabilidades = np.abs(ketfinal)**2

        return probabilidades

    def multrendijascuantico(nrendijas, nubicaciones, matriztrans, estinicial):

        # Cálculo de la matriz de transición ampliada
        matrampliada = np.kron(np.eye(nrendijas), matriztrans)

        # Cálculo de la matriz de proyección
        matrproyeccion = np.zeros((nubicaciones, nrendijas * matriztrans.shape[0]))
        for i in range(nubicaciones):
            matrproyeccion[i, (i+1) * matriztrans.shape[0] - 1] = 1

        # Cálculo del estado final de la partícula
        estfinal = matrproyeccion @ matrampliada @ estinicial

        return estfinal

    def diagramabarras(probabilidades, vectorestados, archivo):

        # Gráfica del diagrama de barras
        plt.bar(range(len(probabilidades)), probabilidades)

        # Ejes del diagrama
        plt.xlabel('Estado')
        plt.ylabel('Probabilidad')

        # Titulo del diagrama
        plt.title('Diagrama de barras de las probabilidades:')

        # Guardar el diagrama y mostrarlo
        plt.savefig(archivo)
        plt.show()
    
`Trabajo realizado por el estudiante Cristian David Polo Garrido.`
