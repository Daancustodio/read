# Sap Hana .net client

## Getting Started
* Clonar projeto SapHanaServiceLayerClient 
* No seu projeto adicione a referência para a SapHanaServiceLayerClient

## Configurar Service Layer end point
* Para acessar os serviços, é necessário informar a URL onde está exposto o servicelayer. 
* Essa informação dever ser inserida na classe estática ServiceLayerSettings.BaseUrl em um ponto de partida do seu projeto
* Exemplo com a classe Program, seria assim:
```
using System;
using SapHanaServiceLayerClient.Service;
namespace HowTo
{
    class Program
    {
        static void Main(string[] args)
        {
            ConfigureServiceLayer();                      
        }

        private static void ConfigureServiceLayer()
        {
            ServiceLayerSettings.BaseUrl = "http://hanab1:50001/b1s/v1";
        }        
    }
}
```

## Autenticação
* Para se autenticar e fazer soliciatções ao service layer:
```
using System;
using SapHanaServiceLayerClient.Service;
namespace HowTo
{
    class Program
    {
        static void Main(string[] args)
        {
            ConfigureServiceLayer();           
            login();
        }

        private static void login()
        {
            IBusinessOneServiceLayer businessOneServiceLayer = new BusinessOneServiceLayer();           
            businessOneServiceLayer.Auth("manager", "password", "CompanyDB");
        }
        private static void ConfigureServiceLayer()
        {
            ServiceLayerSettings.BaseUrl = "http://hanab1:50001/b1s/v1";
        }
    }
}
```
