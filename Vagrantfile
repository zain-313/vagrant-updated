# -*- mode: ruby -*-
# vi: set ft=ruby :
require "yaml"
guests = YAML.load_file("guest_machines.yaml")


configure_machine()

def configure_machine()
  Vagrant.configure("2") do |config|
  guests.each do |guest_vm|
  config.vm.define guest_vm["name"] do |vm|
  set_hostname(guest, guest_vm)
  set_memory(guest, guest_vm)
  set_box(guest, guest_vm)
  run_scripts(guest, guest_vm)
end

def set_hostname(guest, guest_vm)
  vm.vm.hostname = guest_vm["name"]
end


def set_memory(guest, guest_vm)
  vm.vm.provider "virtualbox" do |vb|
  vb.cpus = guest_vm["cpus"]
  vb.memory = guest_vm["memory"]
end

def set_box(guest, guest_vm)
  vm.vm.box = guest_vm["box"]
  vm.vm.network "private_network", ip: guest_vm["private_ip"]
end


def run_scripts(guest, guest_vm)
  guest_vm["scripts"].each do |script|
  vm.vm.provision "shell", path: script
end