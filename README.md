<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>


Enviroment:

Necesita crear el archivo de .env ( puede replicar el archivo .env.example )
y agregar la key de Laravel Nova en la variable de entorno:

    NOVA_LICENSE_KEY=
    
Una vez agregado debera instalar todas las dependencias, tanto de componser como la de los componentes de Nova.
Principalmente la del componente llamado **Onboardingcard**.

    cd nova-components/Onboardingcard && npm run dev
        ó
    npm run build-onboardingcard

Se hizo un cambio en el enfoque, ya que no me parecio apropiado usar una **Nova Tool** para definir el proceso de onboarding,en cambio se hizo la implementacion mediante el uso de una **Card**. El funcionamiento es el mismo pero me parecio mucho mas intuitivo.


Usuario principal para hacer login en el dashboard:

    kevinozmin@gmail.com
    Strongpassword1
