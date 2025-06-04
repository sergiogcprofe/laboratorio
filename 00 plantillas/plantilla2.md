<!-- Plantilla Markdown para Prueba de Concepto -->

<h1 style="color:#0d47a1;">📘 {{ titulo }}</h1>

<p><strong>Versión:</strong> {{ version }}</p>
<p><strong>ID:</strong> {{ id }}</p>
<p><strong>Fecha de creación:</strong> {{ fecha_creacion }}</p>
<p><strong>Última modificación:</strong> {{ fecha_ult_modificacion }}</p>

{% if novedad %}
<p style="color:#ffffff; background-color:#0d47a1; padding:5px; border-radius:5px; display:inline-block;">
  🔵 NUEVA POC
</p>
{% endif %}

---

## 🎯 Objetivo

<p style="color:#000000;">
  {{ objetivo }}
</p>

---

## 🛠️ Tecnologías

<ul>
  {% for tecnologia in tecnologias %}
  <li style="color:#0d47a1;">{{ tecnologia }}</li>
  {% endfor %}
</ul>

---

## 📦 Dependencias

<table style="width:100%; border:1px solid #000000; border-collapse: collapse;">
  <thead style="background-color:#0d47a1; color:#ffffff;">
    <tr>
      <th style="padding:8px; border:1px solid #000000;">Nombre</th>
      <th style="padding:8px; border:1px solid #000000;">Versión</th>
      <th style="padding:8px; border:1px solid #000000;">Notas</th>
    </tr>
  </thead>
  <tbody>
    {% for dep in dependencias %}
    <tr>
      <td style="padding:8px; border:1px solid #000000;">{{ dep.nombre }}</td>
      <td style="padding:8px; border:1px solid #000000;">{{ dep.version }}</td>
      <td style="padding:8px; border:1px solid #000000;">{{ dep.notas }}</td>
    </tr>
    {% endfor %}
  </tbody>
</table>

---

## 🖥️ Entorno

- <strong>Nombre:</strong> {{ entorno.nombre }}
- <strong>Instrucciones:</strong> [Acceder]({{ entorno.instrucciones }})
- <strong>Versiones:</strong>
  <ul>
    {% for ver in entorno.versiones %}
    <li>{{ ver }}</li>
    {% endfor %}
  </ul>
- <strong>Repositorio de entorno:</strong> [Git]({{ entorno.enlace_git_entorno }})

---

## ▶️ Pasos

<ol>
  {% for paso in pasos %}
  <li>{{ paso.descripción }}</li>
  {% endfor %}
</ol>

---

## ✅ Tests

<table style="width:100%; border:1px solid #000000; border-collapse: collapse;">
  <thead style="background-color:#0d47a1; color:#ffffff;">
    <tr>
      <th style="padding:8px; border:1px solid #000000;">#</th>
      <th style="padding:8px; border:1px solid #000000;">Descripción</th>
      <th style="padding:8px; border:1px solid #000000;">Resultado</th>
    </tr>
  </thead>
  <tbody>
    {% for test in tests %}
    <tr>
      <td style="padding:8px; border:1px solid #000000;">{{ test.numero }}</td>
      <td style="padding:8px; border:1px solid #000000;">{{ test.descripción }}</td>
      <td style="padding:8px; border:1px solid #000000;">{{ test.resultado }}</td>
    </tr>
    {% endfor %}
  </tbody>
</table>

---

## 🎥 Videotutorial

🔗 [Ver en YouTube]({{ videotutorial }})

---

## 🔗 Repositorio Git

📁 [Acceder al código]({{ enlace_git }})

---

## 📚 Referencias

<ul>
  {% for ref in referencias %}
  <li><a href="{{ ref.enlace }}" style="color:#0d47a1;">{{ ref.descripción }}</a></li>
  {% endfor %}
</ul>
