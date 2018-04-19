import random
import math
import copy

class Server:
    number = 0
    cpu = 0
    ram = 0
    rate = 0

    def __init__(self, _number, _cpu, _ram):
        self.number = _number
        self.cpu = _cpu
        self.ram = _ram
        self.rate = self.ram/self.cpu




def get_min_server_cnt(vm_data, server_data):
    all_cpu = 0
    all_ram = 0
    length = len(vm_data)
    for i in range(length):
        all_cpu += vm_data[i][1] * vm_data[i][3]
        all_ram += vm_data[i][2] * vm_data[i][3]
    min_in_cpu = math.ceil(all_cpu/server_data[0])
    min_in_ram = math.ceil(all_ram/server_data[1])
    return max(min_in_cpu, min_in_ram)


def init_server_chain_cpu_ram(min_server_cnt, server_data):
    server_chain = []
    for i in range(server_data[0]):
        server_chain.append([])
    for i in range(min_server_cnt):
        server = Server(i+1, server_data[0], server_data[1])
        server_chain[server_data[0]-1].append(server)
    return server_chain


def sort_vm_data_cpu_ram(vm_data):
    tmp = copy.deepcopy(vm_data)
    vm_chain = sorted(tmp, key=lambda x: (x[1], x[2]), reverse=True)
    return vm_chain


def get_types(vm_data):
    length = len(vm_data)
    types = []
    for i in range(length):
        types.append(vm_data[i][0])
    return types


def init_result(min_server_cnt, types):
    result = []
    for i in range(min_server_cnt):
        row = []
        length = len(types)
        for j in range(length):
            row.append([types[j], 0])
        result.append(row)
    return result



def add_server(result, server_chain, server):
    old_row = result[0]
    new_row = []
    length = len(old_row)
    for i in range(length):
        new_row.append([old_row[i], 0])
    result.append(new_row)
    length = len(server_chain)
    server_chain[length - 1].append(server)


def change_result(result, server, vm):
    index = server.number-1
    length = len(result[0])
    for i in range(length):
        if result[index][i][0] == vm[0]:
            result[index][i][1] += 1


def change_server_chain(server_chain, target_i, target_j, vm_cpu, vm_ram):
    server = server_chain[target_i][target_j]
    length = len(server_chain[target_i])
    server_chain[target_i] = server_chain[target_i][0:target_j] + server_chain[target_i][target_j+1:length]
    server.cpu -= vm_cpu
    server.ram -= vm_ram
    if server.cpu != 0 and server.ram != 0:
        server_chain[server.cpu - 1].append(server)
        server_chain[server.cpu - 1].sort(key=lambda x: x.ram, reverse=True)


def change_vm_chain(vm_chain):
    vm_chain[0][3] -= 1
    if vm_chain[0][3] == 0:
        return vm_chain[1:]
    else:
        return vm_chain


def pack_a_cpu_vm(result, vm_chain, server_chain, n, server_data):
    server_chain_start = -1
    length = len(server_chain)
    for i in range(length-1, -1, -1):
        if len(server_chain[i]) != 0:
            server_chain_start = i
            break

    if server_chain_start == -1:
        add_server(result, server_chain, Server(len(result) + 1, server_data[0], server_data[1]))
        return pack_a_cpu_vm(result, vm_chain, server_chain, n, server_data)
    else:
        #print(vm_chain[0])
        vm_cpu = vm_chain[0][1]
        vm_ram = vm_chain[0][2]
        row_min = 0
        row_max = 0
        if (server_chain_start + 1) < vm_cpu:
            add_server(result, server_chain, Server(len(result) + 1, server_data[0], server_data[1]))
            return pack_a_cpu_vm(result, vm_chain, server_chain, n, server_data)
        else:
            locals()
            if server_chain_start <= (n - 1):
                row_min = 0
                row_max = server_chain_start
            else:
                row_min = server_chain_start - n + 1
                row_max = server_chain_start
            row_min = max(vm_cpu - 1, row_min)
            target_i = -1
            target_j = -1
            max_rate = -1

            for i in range(row_min, row_max + 1):
                length = len(server_chain[i])
                for j in range(length):

                    if server_chain[i][j].ram >= vm_ram:

                        rate = server_chain[i][j].rate
                        if rate > max_rate:
                            target_i = i
                            target_j = j
                            max_rate = rate

                        elif rate == max_rate and server_chain[i][j].cpu > server_chain[target_i][target_j].cpu:
                            target_i = i
                            target_j = j
                            max_rate = rate

            if max_rate == -1:
                add_server(result, server_chain, Server(len(result) + 1, server_data[0], server_data[1]))
                return pack_a_cpu_vm(result, vm_chain, server_chain, n, server_data)
            else:
                locals()
                change_result(result, server_chain[target_i][target_j], vm_chain[0], )
                change_server_chain(server_chain, target_i, target_j, vm_cpu, vm_ram)
                vm_chain = change_vm_chain(vm_chain)
                return vm_chain


def get_cpu_use_rate(vm_data, server_data, server_number):
    all_vm_cpu = 0
    length = len(vm_data)

    for i in range(length):
        all_vm_cpu += vm_data[i][1] * vm_data[i][3]

    all_server_cpu = server_data[0] * server_number
    return all_vm_cpu/all_server_cpu


def cpu_pack(vm_number, vm_data, server_data, n):
    min_server_cnt = get_min_server_cnt(vm_data, server_data)
    server_chain = init_server_chain_cpu_ram(min_server_cnt, server_data)
    vm_types = get_types(vm_data)
    vm_chain = sort_vm_data_cpu_ram(vm_data)
    result = init_result(min_server_cnt, vm_types)

    for i in range(vm_number):
        vm_chain = pack_a_cpu_vm(result, vm_chain, server_chain, n, server_data)
    #print(vm_number)
        #print(vm_chain)
    #length_sum = 0
    #for i in range(10, 56):
    #    length_sum += len(server_chain[i])
    #print(length_sum)
    use_rate = get_cpu_use_rate(vm_data, server_data, len(result))

    del_result = []

    if len(result) != 0:
        index = len(result) - 1
        cnt = 0
        for i in range(len(result[index])):
            if result[index][i] != 0:
                cnt += 1
        if cnt <= 3:
            del_result = result[-1:]
            result = result[0:-1]
    return [result, use_rate, del_result]

################


def init_server_chain_ram_cpu(min_server_cnt, server_data):
    server_chain = []
    for i in range(server_data[1]):
        server_chain.append([])
    for i in range(min_server_cnt):
        server = Server(i+1, server_data[0], server_data[1])
        server_chain[server_data[1]-1].append(server)
    return server_chain


def sort_vm_data_ram_cpu(vm_data):
    tmp = copy.deepcopy(vm_data)
    vm_chain = sorted(tmp, key=lambda x: (x[2], x[1]), reverse=True)
    return vm_chain


###


def change_server_chain_ram(server_chain, target_i, target_j, vm_cpu, vm_ram):
    server = server_chain[target_i][target_j]
    length = len(server_chain[target_i])
    server_chain[target_i] = server_chain[target_i][0:target_j] + server_chain[target_i][target_j+1:length]
    server.cpu -= vm_cpu
    server.ram -= vm_ram
    if server.cpu != 0 and server.ram != 0:
        server_chain[server.ram - 1].append(server)
        server_chain[server.ram - 1].sort(key=lambda x: x.cpu, reverse=True)


def pack_a_ram_vm(result, vm_chain, server_chain, n, server_data):
    server_chain_start = -1
    length = len(server_chain)
    for i in range(length-1, -1, -1):
        if len(server_chain[i]) != 0:
            server_chain_start = i
            break

    if server_chain_start == -1:
        add_server(result, server_chain, Server(len(result) + 1, server_data[0], server_data[1]))
        return pack_a_ram_vm(result, vm_chain, server_chain, n, server_data)
    else:
        #print(vm_chain[0])
        vm_cpu = vm_chain[0][1]
        vm_ram = vm_chain[0][2]
        row_min = 0
        row_max = 0
        if (server_chain_start + 1) < vm_ram:
            add_server(result, server_chain, Server(len(result) + 1, server_data[0], server_data[1]))
            return pack_a_ram_vm(result, vm_chain, server_chain, n, server_data)
        else:
            locals()
            if server_chain_start <= (n - 1):
                row_min = 0
                row_max = server_chain_start
            else:
                row_min = server_chain_start - n + 1
                row_max = server_chain_start
            row_min = max(vm_ram - 1, row_min)
            target_i = -1
            target_j = -1
            min_rate = 1000000
            #max_rate = -1###
            for i in range(row_min, row_max + 1):
                length = len(server_chain[i])
                for j in range(length):
                    if server_chain[i][j].cpu >= vm_cpu:
                        rate = server_chain[i][j].rate
                        if rate < min_rate:
                            target_i = i
                            target_j = j
                            min_rate = rate
                        elif rate == min_rate and server_chain[i][j].ram > server_chain[target_i][target_j].ram:
                            target_i = i
                            target_j = j
                            min_rate = rate
                        #if rate > max_rate:
                        #    target_i = i
                        #    target_j = j
                        #    max_rate = rate
                        #elif rate == max_rate and server_chain[i][j].ram > server_chain[target_i][target_j].ram:
                        #    target_i = i
                        #    target_j = j
                        #    max_rate = rate

            if min_rate == 1000000:
            #if max_rate == -1:#
                add_server(result, server_chain, Server(len(result) + 1, server_data[0], server_data[1]))
                return pack_a_ram_vm(result, vm_chain, server_chain, n, server_data)
            else:
                locals()
                change_result(result, server_chain[target_i][target_j], vm_chain[0], )
                change_server_chain_ram(server_chain, target_i, target_j, vm_cpu, vm_ram)
                vm_chain = change_vm_chain(vm_chain)
                return vm_chain


def get_ram_use_rate(vm_data, server_data, server_number):
    all_vm_ram = 0
    length = len(vm_data)

    for i in range(length):
        all_vm_ram += vm_data[i][2] * vm_data[i][3]

    all_server_ram = server_data[1] * server_number
    return all_vm_ram/all_server_ram


def ram_pack(vm_number, vm_data, server_data, n):
    min_server_cnt = get_min_server_cnt(vm_data, server_data)
    server_chain = init_server_chain_ram_cpu(min_server_cnt, server_data)
    vm_types = get_types(vm_data)
    vm_chain = sort_vm_data_ram_cpu(vm_data)
    result = init_result(min_server_cnt, vm_types)

    for i in range(vm_number):
        #print(vm_chain)
        vm_chain = pack_a_ram_vm(result, vm_chain, server_chain, n, server_data)
    #print(vm_number)
    use_rate = get_ram_use_rate(vm_data, server_data, len(result))
    return [result, use_rate]

##################

def pack(vm_number, _vm_data, _server_data, _main_resource, _n):
    _vm_number = 0
    length = len(_vm_data)
    for i in range(length):
        _vm_number += _vm_data[i][3]
    if _main_resource == "cpu":
        #return get_str(cpu_pack(_vm_number, _vm_data, _server_data, _n))
        return cpu_pack(_vm_number, _vm_data, _server_data, _n)[0]
    else:
        #return get_str(ram_pack(_vm_number, _vm_data, _server_data, _n))
        return ram_pack(_vm_number, _vm_data, _server_data, _n)


def get_str(re):
    length = len(re)
    length2 = len(re[0])
    string = str(length) + "\n"
    for i in range(length):
        string += str(i+1)
        for j in range(length2):
            if re[i][j][1] != 0:
                string += " " + re[i][j][0] + " " + str(re[i][j][1])
        string += "\n"
    return string


def get_vm_number():
    return 80


def get_vm_data():
    items = [["flavor1", 1, 1], ["flavor2", 1, 2], ["flavor3", 2, 2], ["flavor4", 2, 4],
             ["flavor5", 4, 8], ["flavor6", 8, 8], ["flavor7", 8, 16], ["flavor8", 1, 4]]
    #items = [["flavor1", 1, 1], ["flavor2", 1, 1], ["flavor3", 8, 8], ["flavor4", 1, 1],
    #         ["flavor5", 2, 2], ["flavor6", 4, 8], ["flavor7", 1, 8], ["flavor8", 1, 8]]
    data = []#27 1 45 59.4   1 1 1  1 1 1 4 8
    for i in range(8):
        cnt = random.randint(1, 50)
        items[i].append(cnt)
        data.append(items[i])
    return data


def get_server_data():
    return [56, 128]


def get_main_resource():
    return "cpu"


if __name__ == "__main__":
    print("hello world")

    re = 0
    for ii in range(100):
        a = pack(get_vm_number(), get_vm_data(), get_server_data(), get_main_resource(), 3)[1]
        print(a)
        re += a
    print(re/100)

