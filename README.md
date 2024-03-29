
# Raycast

Este projeto contém um script de Raycast em C# para Unity.

## Descrição

O script `Raycast.cs` é um componente que pode ser anexado a qualquer objeto do Unity. Ele lança um raio na direção que o objeto está voltado. Se o raio atingir um objeto dentro de uma certa distância, esse objeto será destruído.

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

## Código

Aqui está o código principal:

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Raycast : MonoBehaviour
{
  public float raycast Distance = 20f;

  void Update()
  {
    Ray ray = new Ray(transform.position, transform.forward);
    RaycastHit hitInfo;

    if (Physics.Raycast(ray, out hitInfo, raycastDistance))
    {
      Destroy(hitInfo.collider.gameObject);

      if (hitInfo.collider.CompareTag(Enemy));
      {
        Debug.Log("Voce Destruiu o alvo");
      }
    }
  }
}

