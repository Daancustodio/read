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
        IBusinessOneServiceLayer _businessOneServiceLayer;
        static void Main(string[] args)
        {
            ConfigureServiceLayer();           
            login();
        }

        private static void login()
        {
            this._businessOneServiceLayer = new BusinessOneServiceLayer();           
            this._businessOneServiceLayer.Auth("manager", "password", "CompanyDB");
        }
        private static void ConfigureServiceLayer()
        {
            ServiceLayerSettings.BaseUrl = "http://hanab1:50001/b1s/v1";
        }
    }
}
```

## Consumindo service layer, Inserção e busca de item
```
using System;
using SapHanaServiceLayerClient.Service;
namespace HowTo
{
    class Program
    {
        IBusinessOneServiceLayer _businessOneServiceLayer;
        static void Main(string[] args)
        {
            ConfigureServiceLayer();           
            Login();
            InserItem();
            LoadItem();
        }        
        
        private static void Login()
        {...
        }
        private static void ConfigureServiceLayer()
        { ...           
        }

        private static void InserItem()
        {
            var item = new Item() { ItemCode = "T0099", ItemName = "Descrição do item" };
            var path = ServiceLayerPathEntitiesEnum.Items;
            this._businessOneServiceLayer.Add(path, item);
        }

        private static void LoadItem()
        {
            var item = this._businessOneServiceLayer.GetByIdentity<Item>(this.Path, "T0099");
        }
   
    }

    class Item
    {
        public string ItemCode { get; set; }
        public string ItemName { get; set; }
    }
}
```
