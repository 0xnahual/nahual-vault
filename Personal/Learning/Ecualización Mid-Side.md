---
type: personal
tags: [music-production, eq, fl-studio]
---
La ecualización mid-side sirve para poder ecualizar en mono y en stéreo fácilmente. Para la ecualziación mid-side, se utiliza la herramienta de [[FL Patcher]]

En FL Studio, no existe una herramienta nativa para hacer ecualización mid-side directamente desde un plugin, pero existe una alternativa para hacerlo.

## ¿Cómo hacer ecualización mid-side en FL Studio?
### Paso 1: Agregar el FL Patcher a la lista de Plugins
El Paso 1 es simple, y es simplemente agregar el FL patcher a la lista de Plugins. [[FL Patcher#**¿Para Qué Sirve FL Patcher?**|Para que sirve FL Patcher]]

![[Personal/Learning/FL Patcher.png]]

### Paso 2: 
En el FL Patcher agregar el Plugin de Fruity Stereo Shaper, que servirá para dividir la señal mid y la señal side.

![[Mid Splitter.png]]


### Paso 3: 
Seleccionar 2 outputs del plugin, para poder enviarlo a 2 ecualizadores. Lo que va a hacer es separar el volumen de en medio, con los volumenes de los lados, lo cuál permitirá ecualziar para stéreo y mono respectivamente.

![[Outputs.png]]

### Paso 4
Agregar 2 ecualizadores. El ecualziador de arriba servirá para la ecualziación del side, y la ecualización de abajo servirá para mid. Esto servirá para poder separar la ecualización de mono y de stereo en un mismo mix. Cuando sea stereo, se utilizarán ambos EQ, mientras que cuando sea mono, solo se utilziará el de mid. 

![[2 ecualizadores.png]]