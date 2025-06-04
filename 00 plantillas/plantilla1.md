<!-- PLANTILLA POC PARA GITHUB -->

<h1 style="color:#002B5B; background-color:#E6F0FA; padding:10px;">📘 {{titulo}}</h1>

<p><strong>ID de PoC:</strong> <code>{{id}}</code></p>
<p><strong>Versión:</strong> {{version}}</p>
<p><strong>Fecha de creación:</strong> {{fecha_creacion}}</p>
<p><strong>Última modificación:</strong> {{fecha_ult_modificacion}}</p>

<hr style="border:1px solid #002B5B;">

## 🎯 Objetivo

<p style="color:#000;">{{objetivo}}</p>

---

## ⚙️ Tecnologías Utilizadas

<ul style="color:#002B5B;">
  {{#each tecnologias}}
    <li>{{this}}</li>
  {{/each}}
</ul>

---

## 📦 Dependencias

<table style="width:100%; border:1px solid #002B5B; border-collapse:collapse;">
  <thead style="background-color:#002B5B; color:white;">
    <tr>
      <th style="padding:8px;">Nombre</th>
      <th style="padding:8px;">Versión</th>
      <th style="padding:8px;">Notas</th>
    </tr>
  </thead>
  <tbody>
    {{#each dependencias}}
    <tr style="border:1px solid #ccc;">
      <td style="padding:8px;">{{nombre}}</td>
      <td style="padding:8px;">{{version}}</td>
      <td style="padding:8px;">{{notas}}</td>
    </tr>
    {{/each}}
  </tbody>
</table>

---

## 🖥️ Entorno

<p><strong>Nombre:</strong> {{entorno.nombre}}</p>
<p><strong>Instrucciones:</strong> <a href="{{entorno.instrucciones}}" style="color:#002B5B;">Guía de instalación</a></p>
<p><strong>Versiones:</strong></p>
<ul>
  {{#each entorno.versiones}}
    <li>{{this}}</li>
  {{/each}}
</ul>
<p><strong>Repositorio:</strong> <a href="{{entorno.enlace_git_entorno}}" style="color:#002B5B;">Ver en Git</a></p>

---

## 🔧 Pasos para la Implementación

<ol>
  {{#each pasos}}
    <li><strong>Paso {{numero}}:</strong> {{descripción}}</li>
  {{/each}}
</ol>

---

## ✅ Tests Realizados

<ol>
  {{#each tests}}
    <li>
      <p><strong>Test {{numero}}:</strong> {{descripción}}</p>
      <p><strong>Resultado:</strong> {{resultado}}</p>
    </li>
  {{/each}}
</ol>

---

## 📚 Referencias

<ul>
  {{#each referencias}}
    <li><a href="{{enlace}}" target="_blank" style="color:#002B5B;">{{descripción}}</a></li>
  {{/each}}
</ul>

---

## 🎥 Videotutorial

<p>
  <a href="{{videotutorial}}" style="color:#002B5B;">Ver en YouTube</a>
</p>

---

## 🔗 Repositorio GitHub

<p>
  <a href="{{enlace_git}}" style="color:#002B5B;">Acceder al código fuente</a>
</p>

---

<sub style="color:#aaa;">Esta PoC fue generada como plantilla para futuros desarrollos técnicos.</sub>
