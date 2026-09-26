# PROJECT_CONTEXT — SOLQARYN

> Contexto técnico canónico de estado actual. Este archivo describe únicamente la realidad vigente necesaria para trabajar sobre SOLQARYN.

## 1. Identidad y repositorio

- PROJECT_ID: `SOLQARYN`
- PROJECT_SCOPE_LOCK: `STRICT`
- `PROJECT_SCOPE_LOCK=STRICT`
- Plataforma: SOLQARYN.
- Repositorio: `solqaryn/Solqaryn`.
- Rama ordinaria de trabajo: `dev`.
- Rama productiva: `main`; cualquier cambio requiere autorización explícita vigente.
- GitHub Environments canónicos: `DEV` y `PROD`.
- Identidad corporativa operativa: `solqaryn.platform@outlook.com`.
- VariStoreHN es una empresa cliente alojada en SOLQARYN; no define la identidad de la plataforma.

## 2. Regla de estado vivo

Antes de actuar:

1. leer `docs/VAEP_AUTHORITY.md`;
2. releer HEAD vivo de `dev`;
3. consultar sólo el estado operativo necesario para la tarea;
4. validar dependencias técnicas reales del scope;
5. usar CI/tests/readbacks causales cuando corresponda.

Ningún plan, fila, gate, fase o secuencia que no esté incorporado al MAESTRO vigente puede condicionar trabajo nuevo.

## 3. Arquitectura vigente

SOLQARYN es una plataforma empresarial multiempresa.

- Frontend: Angular 20 standalone, Signals y Angular Material.
- Backend: ASP.NET Core 8 Web API.
- Capas: Domain <- Application <- Infrastructure; API compone y expone.
- Persistencia: MySQL con EF Core 8/Pomelo.
- Seguridad: JWT, BCrypt, RBAC relacional, auditoría, CORS explícito, rate limiting y security headers.
- Integraciones vigentes: Cloudinary, QuestPDF y SMTP.
- E2E/browser: Playwright/Chromium.
- La autorización del backend es la autoridad; la UI nunca sustituye controles de seguridad.
- Tenancy, integridad transaccional y trazabilidad deben preservarse en cambios de negocio.

Consultar `ARCHITECTURE.md` para cambios estructurales y `PROJECT_INDEX.md` para navegación dirigida.

## 4. Infraestructura canónica

### GitHub
- Repositorio: `solqaryn/Solqaryn`.
- Trabajo: `dev`.
- Environments: `DEV` y `PROD`.

### Render
- DEV: `solqaryn-api-dev`, rama `dev`, health `/health/ready`, base `solqaryn_dev`.
- PROD corporativo: `solqaryn-api-prod`, rama `main`.
- El runtime PROD está conectado a la base canónica `solqaryn_prod`.
- `Database__ApplyMigrationsOnStartup=false` mientras la base PROD se prepara y antes de migrar el respaldo legacy.
- Cloudinary runtime PROD usa cloud corporativo `riyrzmob` con prefijo `solqaryn_prod`.
- La configuración declarativa de `render.yaml` define para PROD el mismo Dockerfile/health policy de DEV; el control-plane del servicio existente requiere readback y ajuste manual si todavía conserva settings anteriores.

### Vercel
- DEV: `solqaryn-dev`.
- PROD objetivo: `solqaryn-prod`, rama `main`, root `frontend`.
- El frontend ya contiene routing para `solqaryn-prod.vercel.app`, `solqaryn.com` y `www.solqaryn.com` hacia `solqaryn-api-prod.onrender.com`.
- La creación/enlace del proyecto PROD permanece pendiente mientras el conector disponible no exponga creación de proyectos.

### Aiven
- Proyecto: `solqaryn`.
- Servicio MySQL: `solqaryn-mysql`.
- Bases: `solqaryn_dev` y `solqaryn_prod`.
- Usuarios de aplicación separados por entorno.
- Estado certificado de `solqaryn_prod` antes de migrar el respaldo: 0 tablas, 0 migraciones EF, 0 empresas, 0 productos y 0 usuarios.
- El respaldo productivo legacy permanece separado y no debe restaurarse hasta completar y certificar la infraestructura PROD.

### Cloudflare
- Dominio objetivo: `solqaryn.com`.
- DNS/cutover público se ejecuta después de crear y certificar Vercel PROD; no se debe desviar tráfico antes de esa certificación.

## 5. Dominios funcionales

Áreas principales:

- empresas y configuración empresarial;
- autenticación, usuarios, roles y permisos;
- productos, variantes, catálogos e imágenes;
- inventario, almacenes, ubicaciones, reservas y movimientos;
- compras, proveedores y cuentas por pagar;
- ventas, clientes, cotizaciones, pedidos y facturación;
- finanzas;
- descuentos e impuestos;
- auditoría;
- reportes;
- tienda pública de empresas cliente;
- automatizaciones de operación y control.

## 6. Invariantes

- No exponer secretos.
- No mezclar datos entre empresas.
- No confiar en permisos visuales como sustituto del backend.
- Migraciones y cambios de datos deben ser explícitos, verificables y recuperables.
- No force-push.
- Revalidar HEAD antes de publicar.
- Cambios en `main`, PROD o infraestructura productiva requieren autorización explícita vigente.

## 7. Plan maestro vigente

El plan maestro que ejecutan las diez automatizaciones se define únicamente por objetivos, prioridades y dependencias actuales de SOLQARYN.

No hereda restricciones, numeraciones, fases, filas, gates ni prioridades que no hayan sido incorporadas expresamente a la versión vigente del MAESTRO.

La implementación existente puede ser modificada, reemplazada o retirada cuando el objetivo vigente lo requiera, siempre bajo controles de seguridad, integridad, trazabilidad, revisión y rollback proporcionales.
