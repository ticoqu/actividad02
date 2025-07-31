# Actividad 2: Configuración inicial de proveedor Proxmox

## Descripción
En esta actividad configurarás Terraform para conectarse con un clúster Proxmox. Esto implica definir el proveedor Telmate/proxmox y sus credenciales.

## Requisitos
- Terraform instalado (Actividad 1).
- Acceso a un servidor Proxmox con permisos de API.

### 🎯 Objetivo
Configurar Terraform para conectarse con un entorno Proxmox.

### Entrega
Incluir captura de pantalla del resultado de terraform init.

## Pasos a seguir

**1. Crear un usuario en Proxmox**

Ir a: Datacenter → Permissions → Users → Add

- Crear un usuario: terraform@pve
- Realm: PVE
- Password: contrasenia
- Expire: nunca

**2. Crear un rol limitado**
Ir a: Datacenter → Permissions → Roles → Add
Crear el rol TerraformRole con estas privilegios:
VM.Audit
VM.Console
VM.Monitor
VM.PowerMgmt
VM.Config.Disk
VM.Config.CPU
VM.Config.Memory
VM.Config.Network
VM.Allocate
Datastore.AllocateSpace
Datastore.Audit
Sys.Audit

Este rol permitirá:

- Crear/modificar/manejar VMs
- Leer y auditar nodos y almacenamiento

**3. Asignar el rol al usuario**
Ir a: Datacenter → Permissions → Add

User: terraform@pve
Role: TerraformRole

Propagate: (para aplicar recursivamente)

**4. Verificar que el usuario puede usar la API**
curl -k -d "username=terraform@pve&password=TU_PASSWORD" https://PROXMOX_IP:8006/api2/json/access/ticket

Respuesta JSON con un ticket de sesión y CSRF token.


1. **Crear el archivo providers.tf**
   ```bash
      terraform {
     required_providers {
       proxmox = {
         source = "Telmate/proxmox"
         version = "3.0.1-rc3"
       }
     }
   }

   provider "proxmox" {
     pm_tls_insecure      = true
     pm_api_url           = "https://localhost:8006/api2/json"
     pm_api_token_id      = "terra@pve!te"
     pm_api_token_secret  = "69622"
   }
   ```
   
2. **Inicializar Terraform**
   ```bash
   terraform init
   ```

3. **Verificar conexión**
   ```bash
   terraform plan
   ```
7. **Opcional: Configurar autocompletado**
   ```bash
   terraform -install-autocomplete
   ```
