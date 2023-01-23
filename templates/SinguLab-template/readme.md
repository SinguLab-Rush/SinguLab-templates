# SinguLab Template

During workspace creation, Coder prompts you to specify a dotfiles URL via a Terraform variable. Once the 
workspace starts, the Coder agent runs `yadm clone --recurse-submodules` via the startup script:


````HCF
variable "dotfiles_uri" {
  description = <<-EOF
  Dotfiles repo URI (optional)
  see https://dotfiles.github.io
  EOF
  default     = "https://github.com/pranavmishra90/dotfiles"
}

resource "coder_agent" "main" {
  arch           = data.coder_provisioner.me.arch
  os             = "linux"
  startup_script = var.dotfiles_uri != "" ? "yadm clone --recurse-submodules -f ${var.dotfiles_uri}" : null
}

````

The latest SinguLab image is pulled from DockerHub:

````HCF
variable "docker_image" {
  default = "pranavmishra90/datascience:latest"
}
````

