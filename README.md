# Actividad 1: Instalación de Terraform en Debian

## Descripción
En esta actividad aprenderás a instalar Terraform en un sistema operativo Debian, lo cual es fundamental para automatizar el despliegue de infraestructura en entornos como Proxmox.

## Requisitos
- Máquina virtual o servidor con Debian instalado.
- Acceso a internet.

## Objetivo
Instalar Terraform y verificar su funcionamiento.

## Entrega
Captura de pantalla del resultado de `terraform --version`.

## Pasos a seguir

1. **Actualizar el sistema**
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```
   
2. **Instalar dependencias necesarias**
   ```bash
   sudo apt install -y curl wget gnupg software-properties-common
   ```

3. **Descargar e instalar Terraform - Descarga la última versión estable:**
   ```bash
   wget https://releases.hashicorp.com/terraform/1.7.5/terraform_1.7.5_linux_amd64.zip
   ```
   
   Descomprime el archivo:
   ```bash
   unzip terraform_1.7.5_linux_amd64.zip
   ```
   
   Mueve el binario al directorio /usr/local/bin/:
   ```bash
   sudo mv terraform /usr/local/bin/
   ```

5. **Verificar la instalación**
   ```bash
   terraform --version
   ```
   
7. **Opcional: Configurar autocompletado**
   ```bash
   terraform -install-autocomplete
   ```
