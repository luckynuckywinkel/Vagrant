# -*- mode: ruby -*-
# vi: set ft=ruby :

# VM array
# Массив виртмашин
virt_machines=[
  {
    :hostname => "kuber1",
  },
  {
    :hostname => "kuber2",
  }
]

# Show VM GUI
# Показывать гуй виртмашины
HOST_SHOW_GUI = true 

# VM RAM
# Оперативная память ВМ
HOST_MEMMORY = "1024" 

# VM vCPU
# Количество ядер ВМ
HOST_CPUS = 1

# Network adapter to bridge
# В какой сетевой адаптер делать бридж
HOST_BRIDGE = "Intel(R) Ethernet Connection I219-LM"

# Which box to use
# Из какого бокса выкатываемся
HOST_VM_BOX = "generic/debian10" 

################################################
# Parameters passed to provision script
# Параметры передаваемые в скрипт инициализации
################################################

# Script to use while provisioning
# Скрипт который будет запущен в процессе настройки
HOST_CONFIIG_SCRIPT = "script.sh" 

# Additional user
# Дополнительный пользователь
HOST_USER = 'test'

# Additional user pass. Root pass will be same
# Пароль дополнительного пользователя. Пароль рута будет таким же
HOST_USER_PASS = '123456789' 

# Run apt dist-upgrade
# Выполнить apt dist-upgrade
HOST_UPGRADE = 'false' 

Vagrant.configure("2") do |config|
	virt_machines.each do |machine|
		config.vm.box = HOST_VM_BOX
		config.vm.define machine[:hostname] do |node|
			node.vm.hostname = machine[:hostname]
			node.vm.network :public_network, bridge: HOST_BRIDGE
			node.vm.provider "virtualbox" do |current_vm, override|
				current_vm.name = machine[:hostname]
				current_vm.gui = HOST_SHOW_GUI
				current_vm.memory = HOST_MEMMORY
				current_vm.cpus = HOST_CPUS
				override.vm.provision "shell", path: 'script.sh', args: [	'test', 	'123456789',	'false', 	machine[:hostname]   ], run: "once"
			end
		end
	end
end
