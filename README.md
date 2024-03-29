

# Projeto Raycast

Este projeto contém um script de Raycast em C# para Unity.

## Descrição

- Kauã de Castro(KalCastro)
- Vincenzo Monaco(VincenMonaco)

O script `Raycast.cs` é um componente que pode ser anexado a qualquer objeto do Unity. Ele lança um raio na direção que o objeto está voltado. Se o raio atingir um objeto dentro de uma certa distância, esse objeto será destruído.

## Autores

## Detalhes do Código

O código funciona da seguinte maneira:

1. `public float raycast Distance = 20f;`: Esta linha define a distância máxima que o raio pode atingir. Você pode ajustar este valor no inspetor do Unity.

2. `void Update()`: Esta função é chamada uma vez por frame. O código dentro desta função é executado continuamente.

3. `Ray ray = new Ray(transform.position, transform.forward);`: Aqui, um novo raio é criado. O raio começa na posição do objeto e vai na direção em que o objeto está voltado.

4. `RaycastHit hitInfo;`: Esta linha cria uma variável para armazenar informações sobre o que o raio atinge.

5. `if (Physics.Raycast(ray, out hitInfo, raycastDistance))`: Esta linha lança o raio. Se o raio atingir algo dentro da distância definida, a informação do objeto atingido é armazenada em `hitInfo`.

6. `Destroy(hitInfo.collider.gameObject);`: Se o raio atingir um objeto, esse objeto é destruído.

7. `if (hitInfo.collider.CompareTag(Enemy));`: Esta linha verifica se o objeto destruído tem a tag "Enemy".

8. `Debug.Log("Voce Destruiu o alvo");`: Se o objeto destruído tinha a tag "Enemy", uma mensagem é registrada no console do Unity.

## Código Raycast
```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class _Camera : MonoBehaviour
{
    public float raycastDistance = 20f;

    void Update()
    {
        Ray ray = new Ray(transform.position, transform.forward);
        RaycastHit hitInfo;

        if (Physics.Raycast(ray, out hitInfo, raycastDistance))
        {
            Destroy(hitInfo.collider.gameObject);

            if (hitInfo.collider.CompareTag("Enemy")) ;
            {
                Debug.Log("Voce Destruiu o alvo");
            }
        }
    }
}
```

# Câmera

Este código contem um script de câmera em C# para Unity.

## Descrição

O script `Camera.cs` é um componente que pode ser anexado a qualquer objeto do Unity para controlar a rotação da câmera com base no movimento do mouse.

## Detalhes do Código

O código funciona da seguinte maneira:

1. `public enum RotationAxes { MouseXAndY = 0, MouseX = 1, MouseY = 2 }`: Este enum define os eixos de rotação que a câmera pode usar.

2. `public RotationAxes axes = RotationAxes.MouseXAndY;`: Aqui, definimos o eixo de rotação padrão como `MouseXAndY`.

3. `public float sensitivityHor = 5.0f;` e `public float sensitivityVert = 5.0f;`: Estas linhas definem a sensibilidade da rotação horizontal e vertical, respectivamente.

4. `public float minimumVert = -45.0f;` e `public float maximumVert = 45.0f;`: Estas linhas definem os limites de rotação vertical.

5. `private float _rotationX = 0;`: Esta linha define uma variável privada para armazenar a rotação atual no eixo X.

6. `void Start()`: Esta função é chamada no início. Aqui, verificamos se o objeto tem um componente Rigidbody e, se tiver, congelamos a rotação.

7. `void Update()`: Esta função é chamada uma vez por frame. Aqui, verificamos qual eixo de rotação está definido e ajustamos a rotação do objeto com base no movimento do mouse.

## Código

Aqui está o código principal:

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Camera : MonoBehaviour
{
    
    public enum RotationAxes
    {
        MouseXAndY = 0,
        MouseX = 1,
        MouseY = 2
    }
    
    public RotationAxes axes = RotationAxes.MouseXAndY;
    
    public float sensitivityHor = 5.0f;
    public float sensitivityVert = 5.0f;
    
    public float minimumVert = -45.0f;
    public float maximumVert = 45.0f;
    
    private float _rotationX = 0;
    void Start()
    {
        
        Rigidbody body = GetComponent<Rigidbody>();
        if (body != null)
            body.freezeRotation = true;
    }
    void Update()
    {
        if (axes == RotationAxes.MouseX)
        {
            transform.Rotate(0, Input.GetAxis("Mouse X") * sensitivityHor, 0);
        }
        else if (axes == RotationAxes.MouseY)
        {
            _rotationX -= Input.GetAxis("Mouse Y") * sensitivityVert;
            _rotationX = Mathf.Clamp(_rotationX, minimumVert, maximumVert);
            float rotationY = transform.localEulerAngles.y;
            
            transform.localEulerAngles = new Vector3(_rotationX, rotationY, 0);
        }
        else
        {
            _rotationX -= Input.GetAxis("Mouse Y") * sensitivityVert;
            _rotationX = Mathf.Clamp(_rotationX, minimumVert, maximumVert);
            float delta = Input.GetAxis("Mouse X") * sensitivityHor;
            float rotationY = transform.localEulerAngles.y + delta;
            transform.localEulerAngles = new Vector3(_rotationX, rotationY, 0);
        }
    }
}

```

## Demonstração por video





