import datetime
import math
import random


def transdate(aim):
    res = aim.split('-')
    return datetime.date(int(res[0]), int(res[1]), int(res[2]))


def datapreparition(dataset, look_back=1):
    dataX, dataY = [], []
    for i in xrange(len(dataset) - look_back - 1):
        a = dataset[i:(i + look_back)]
        dataX.append(a)
        dataY.append([dataset[i + look_back]])
    return dataX, dataY


def getdata(focus, traindata_count, days):
    focus_count = [0] * days
    for i in xrange(days):
        if focus in traindata_count[i]:
            if i != 0:
                focus_count[i] = traindata_count[i][focus]
            else:
                focus_count[i] = traindata_count[i][focus]
        else:
            if i != 0:
                focus_count[i] = 0
    return focus_count
    # pyplot.plot(focus_count, label=focus)


class scaler:
    def __init__(self):
        self.valmin = 0
        self.valmax = 0

    def scale(self, aim):
        self.valmin = float(min(aim))
        self.valmax = float(max(aim))

        if self.valmin == self.valmax:
            return aim

        for i in xrange(len(aim)):
            aim[i] = (float(aim[i]) - self.valmin) / (self.valmax - self.valmin)

        return aim

    def recover(self, aim):

        for i in xrange(len(aim)):
            aim[i] = aim[i] * (self.valmax - self.valmin) + self.valmin

        return aim

    def recover_out(self, aim):
        pre_out = []
        for x in aim:
            for y in x:
                pre_out.append(int(math.floor(y * (self.valmax - self.valmin) + self.valmin)))
        return pre_out


def getdata_sum(focus, traindata_count, days):
    focus_count = [0] * days
    for i in xrange(days):
        if focus in traindata_count[i]:
            if i != 0:
                focus_count[i] = traindata_count[i][focus] + focus_count[i - 1]
            else:
                focus_count[i] = traindata_count[i][focus]
        else:
            if i != 0:
                focus_count[i] = focus_count[i - 1]
    return focus_count


###wrl start
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
        self.rate = self.ram / self.cpu


def get_min_server_cnt(vm_data, server_data):
    all_cpu = 0
    all_ram = 0
    length = len(vm_data)
    for i in xrange(length):
        all_cpu += vm_data[i][1] * vm_data[i][3]
        all_ram += vm_data[i][2] * vm_data[i][3]
    min_in_cpu = math.ceil((float(all_cpu) / server_data[0]))
    min_in_ram = math.ceil((float(all_ram) / server_data[1]))
    # print("min_in_cpu " + str(min_in_cpu))
    # print("min_in_ram " + str(min_in_ram))
    return int(max(min_in_cpu, min_in_ram))


def init_server_chain_cpu_ram(min_server_cnt, server_data):
    server_chain = []
    for i in xrange(server_data[0]):
        server_chain.append([])
    # print(min_server_cnt)#########
    for i in xrange(min_server_cnt):
        server = Server(i + 1, server_data[0], server_data[1])
        server_chain[server_data[0] - 1].append(server)
    return server_chain


def sort_vm_data_cpu_ram(vm_data):
    tmp = copy.deepcopy(vm_data)
    vm_chain = sorted(tmp, key=lambda x: (x[1], x[2]), reverse=True)
    flage = True
    while (flage):
        flage = False
        length = len(vm_chain)
        for i in xrange(length):
            if vm_chain[i][3] == 0:
                vm_chain = vm_chain[0:i] + vm_chain[i + 1:length]
                flage = True
                break
    # print "sorted:" + str(vm_chain)
    return vm_chain


def get_types(vm_data):
    length = len(vm_data)
    types = []
    for i in xrange(length):
        types.append(vm_data[i][0])
    return types


def init_result(min_server_cnt, types):
    result = []
    for i in xrange(min_server_cnt):
        row = []
        length = len(types)
        for j in xrange(length):
            row.append([types[j], 0])
        result.append(row)
    return result


def add_server(result, server_chain, server):
    old_row = result[0]
    new_row = []
    length = len(old_row)
    for i in xrange(length):
        new_row.append([old_row[i], 0])
    result.append(new_row)
    length = len(server_chain)
    server_chain[length - 1].append(server)


def change_result(result, server, vm):
    index = server.number - 1
    length = len(result[0])
    for i in xrange(length):
        if result[index][i][0] == vm[0]:
            result[index][i][1] += 1


def change_server_chain(server_chain, target_i, target_j, vm_cpu, vm_ram):
    server = server_chain[target_i][target_j]
    length = len(server_chain[target_i])
    server_chain[target_i] = server_chain[target_i][0:target_j] + server_chain[target_i][target_j + 1:length]
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
    for i in xrange(length - 1, -1, -1):
        if len(server_chain[i]) != 0:
            server_chain_start = i
            break

    if server_chain_start == -1:
        add_server(result, server_chain, Server(len(result) + 1, server_data[0], server_data[1]))
        return pack_a_cpu_vm(result, vm_chain, server_chain, n, server_data)
    else:
        # print(vm_chain[0])
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

            for i in xrange(row_min, row_max + 1):
                length = len(server_chain[i])
                for j in xrange(length):

                    if server_chain[i][j].ram >= vm_ram:

                        rate = server_chain[i][j].rate
                        if rate > max_rate:
                            target_i = i
                            target_j = j
                            max_rate = rate
                            # print("rate > max_rate")

                        elif rate == max_rate and server_chain[i][j].cpu > server_chain[target_i][target_j].cpu:
                            target_i = i
                            target_j = j
                            max_rate = rate
                            # print("rate == max_rate")

            if max_rate == -1:
                add_server(result, server_chain, Server(len(result) + 1, server_data[0], server_data[1]))
                # print(len(result))
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

    for i in xrange(length):
        all_vm_cpu += vm_data[i][1] * vm_data[i][3]

    all_server_cpu = server_data[0] * server_number
    return all_vm_cpu / all_server_cpu


def cpu_pack(vm_number, vm_data, server_data, n, answer):
    min_server_cnt = get_min_server_cnt(vm_data, server_data)
    if min_server_cnt != 0:
        server_chain = init_server_chain_cpu_ram(min_server_cnt, server_data)
        vm_types = get_types(vm_data)
        vm_chain = sort_vm_data_cpu_ram(vm_data)
        result = init_result(min_server_cnt, vm_types)

        for i in xrange(vm_number):
            vm_chain = pack_a_cpu_vm(result, vm_chain, server_chain, n, server_data)
            # print(vm_number)
            # print(vm_chain)
        # use_rate = get_cpu_use_rate(vm_data, server_data, len(result))

        del_result = []
        if len(result) != 0:
            index = len(result) - 1
            cnt = 0
            for i in xrange(len(result[index])):
                if result[index][i][1] != 0:
                    cnt += result[index][i][1]
                    del_result.append([result[index][i][0], result[index][i][1]])
            if cnt <= 3:
                result = result[0:-1]
                for i in xrange(len(del_result)):
                    for j in xrange(len(answer)):
                        if answer[j].split(' ')[0] == del_result[i][0]:
                            num = int(answer[j].split(' ')[1]) - del_result[i][1]
                            answer[j] = del_result[i][0] + ' ' + str(num)
                            break

        return result

    else:
        return []


#######################
# not ready


def init_server_chain_ram_cpu(min_server_cnt, server_data):
    server_chain = []
    for i in xrange(server_data[1]):
        server_chain.append([])
    for i in xrange(min_server_cnt):
        server = Server(i + 1, server_data[0], server_data[1])
        server_chain[server_data[1] - 1].append(server)
    return server_chain


def sort_vm_data_ram_cpu(vm_data):
    tmp = copy.deepcopy(vm_data)
    vm_chain = sorted(tmp, key=lambda x: (x[2], x[1]), reverse=True)
    flage = True
    while (flage):
        flage = False
        length = len(vm_chain)
        for i in xrange(length):
            if vm_chain[i][3] == 0:
                vm_chain = vm_chain[0:i] + vm_chain[i + 1:length]
                flage = True
                break
    # print "sorted:" + str(vm_chain)
    return vm_chain


###


def change_server_chain_ram(server_chain, target_i, target_j, vm_cpu, vm_ram):
    server = server_chain[target_i][target_j]
    length = len(server_chain[target_i])
    server_chain[target_i] = server_chain[target_i][0:target_j] + server_chain[target_i][target_j + 1:length]
    server.cpu -= vm_cpu
    server.ram -= vm_ram
    if server.cpu != 0 and server.ram != 0:
        server_chain[server.ram - 1].append(server)
        server_chain[server.ram - 1].sort(key=lambda x: x.cpu, reverse=True)


def pack_a_ram_vm(result, vm_chain, server_chain, n, server_data):
    server_chain_start = -1
    length = len(server_chain)
    for i in xrange(length - 1, -1, -1):
        if len(server_chain[i]) != 0:
            server_chain_start = i
            break

    if server_chain_start == -1:
        add_server(result, server_chain, Server(len(result) + 1, server_data[0], server_data[1]))
        return pack_a_ram_vm(result, vm_chain, server_chain, n, server_data)
    else:
        # print(vm_chain[0])
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

            for i in xrange(row_min, row_max + 1):
                length = len(server_chain[i])
                for j in xrange(length):
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

            if min_rate == 1000000:
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

    for i in xrange(length):
        all_vm_ram += vm_data[i][2] * vm_data[i][3]

    all_server_ram = server_data[1] * server_number
    return all_vm_ram / all_server_ram


def ram_pack(vm_number, vm_data, server_data, n, answer):
    min_server_cnt = get_min_server_cnt(vm_data, server_data)
    if min_server_cnt != 0:
        server_chain = init_server_chain_ram_cpu(min_server_cnt, server_data)
        vm_types = get_types(vm_data)
        vm_chain = sort_vm_data_ram_cpu(vm_data)
        result = init_result(min_server_cnt, vm_types)

        for i in xrange(vm_number):
            # print(vm_chain)
            vm_chain = pack_a_ram_vm(result, vm_chain, server_chain, n, server_data)
        # print(vm_number)
        # use_rate = get_ram_use_rate(vm_data, server_data, len(result))

        del_result = []
        if len(result) != 0:
            index = len(result) - 1
            cnt = 0
            for i in xrange(len(result[index])):
                if result[index][i][1] != 0:
                    cnt += result[index][i][1]
                    del_result.append([result[index][i][0], result[index][i][1]])
            if cnt <= 3:
                result = result[0:-1]
                for i in xrange(len(del_result)):
                    for j in xrange(len(answer)):
                        if answer[j].split(' ')[0] == del_result[i][0]:
                            num = int(answer[j].split(' ')[1]) - del_result[i][1]
                            answer[j] = del_result[i][0] + ' ' + str(num)
                            break
        return result
    else:
        return []


def get_str(re):
    length = len(re)
    if length == 0:
        return ["0"]
    str_list = list()
    str_list.append(str(length))
    length2 = len(re[0])

    for i in xrange(length):
        string = str(i + 1)
        for j in xrange(length2):
            if re[i][j][1] != 0:
                string += " " + re[i][j][0] + " " + str(re[i][j][1])
        str_list.append(string)
    return str_list


##############

def pack(vm_number, _vm_data, _server_data, _main_resource, answer, _n=3):
    _vm_number = 0
    length = len(_vm_data)
    for i in xrange(length):
        _vm_number += _vm_data[i][3]
    # print("["+_main_resource+"]")
    # print("vm number " + str(_vm_number))

    if _main_resource == "CPU":
        # print("cpu")
        step2 = get_str(cpu_pack(_vm_number, _vm_data, _server_data, _n, answer))
        answer += step2
    else:
        # print("ram")
        step2 = get_str(ram_pack(_vm_number, _vm_data, _server_data, _n, answer))
        answer += step2

###wrl end

def pack_dp(vm_number, _vm_data, _server_data, _main_resource):
    print  _vm_data
    se_cpu = _server_data[0]
    se_mem = _server_data[1]
    vm_status = [x[3] for x in _vm_data]
    n = len(_vm_data)
    f = [[0 for i in xrange(se_mem+1)] for j in xrange(se_cpu+1)]
    path = [[[0 for i in xrange(se_mem+1)] for j in xrange(se_cpu+1)] for k in xrange(n+1)]
    flag = True
    phy_use = 0
    records = []
    answer = []
    while flag :
        for i in xrange(n):
            vm_cpu  = _vm_data[i][1]
            vm_mem  = _vm_data[i][2]
            for j in xrange(_vm_data[i][3]):
                for k in xrange(se_cpu, vm_cpu*j, -1):
                    for p in xrange(se_mem, vm_mem*j, -1):
                        if(f[k][p]< f[k-vm_cpu*j][p-vm_mem*j]+1):
                            f[k][p] = f[k-vm_cpu*j][p-vm_mem*j]+1
                            path[i][k][p] = 1
        i = n
        j = se_cpu
        k = se_mem
        putin = 0
        #print "pack answer:"
        fla_record = [0 for x in _vm_data]
        while (i>=0 and j>=0 and k>=0):
            if (path[i][j][k] == 1 and vm_status[i]>0) :
                fla_record[i] += 1
                putin+=1
                j -= _vm_data[i][1]
                k -= _vm_data[i][2]
                vm_status[i]-=1
            else:
                i-=1
        if putin>0:
            phy_use+=1
            records.append(fla_record)
        count = 0
        for x in vm_status:
            count+=x
        if count == 0:
            flag = False
    answer.append(int(phy_use))
    #print records
    for j in xrange(phy_use):
        an = str(j + 1)
        for k in xrange(len(records[j])):
            if records[j][k]!=0:
                an += ' ' + str(_vm_data[k][0]) + ' '
                an += str(records[j][k])
        answer.append(an)
    #print answer



    return answer

def packing(vm_number, _vm_data, _server_data, _main_resource):
    phy_use = 0
    phy_status = []
    se_cpu = _server_data[0]
    se_mem = _server_data[1]
    phy_ans = []
    answer = []
    # print _vm_data
    for x in _vm_data:
        vm_type = x[0]
        vm_cpu = x[1]
        vm_mem = x[2]
        for num in xrange(x[3]):
            # print vm_type
            putin = 0
            for i in xrange(phy_use):
                if phy_status[i][0] >= vm_cpu and phy_status[i][1] >= vm_mem:
                    putin = 1
                    phy_status[i][0] -= vm_cpu
                    phy_status[i][1] -= vm_mem
                    if vm_type not in phy_ans[i]:
                        phy_ans[i][vm_type] = 1
                    else:
                        phy_ans[i][vm_type] += 1
                    break
            if putin == 0:
                phy_use += 1
                phy_status.append([se_cpu - vm_cpu, se_mem - vm_mem])
                phy_ans.append({vm_type: 1})
    answer.append(str(phy_use))
    for j in xrange(phy_use):
        an = str(j + 1)
        for k in phy_ans[j]:
            # print "k: %s" %k
            an += ' ' + str(k) + ' '
            an += str(phy_ans[j][k])
        answer.append(an)
        # print answer
    return answer


def knn_dis(a, b):
    suma = 0.0
    sumb = 0.0
    ans = 0.0
    for i in xrange(len(a)):
        ans += (a[i] - b[i]) * (a[i] - b[i])
    return math.sqrt(ans)


def knn_predict(data, lookback, k):
    length = len(data)
    record = []
    # print data
    vec_aim = [data[i] for i in xrange(length - lookback, length - 1)]
    for i in xrange(length - lookback - 1):
        vec_now = [data[j] for j in xrange(i, i + lookback)]
        dis = knn_dis(vec_aim, vec_now)
        if len(record) < k:
            record.append([i, dis, data[i + lookback - 1]])
        else:
            for j in xrange(len(record)):
                if dis < record[j][1]:
                    record[j] = [i, dis, data[i + lookback - 1]]
                    break
    ans = 0.0
    for i in xrange(len(record)):
        ans += record[i][2]
    # print "record: {0}".format(record)
    # print "ans : %d , len(record): %d" % (ans, len(record))
    return ans / float(len(record))


def predict_vm(ecs_lines, input_lines):
    # Do your work from here#
    starttime = datetime.datetime.now()
    result = []
    if ecs_lines is None:
        print 'ecs information is none'
        return result
    if input_lines is None:
        print 'input file information is none'
        return result
    ps_cpus = 0
    ps_mem = 0
    ps_hdd = 0
    # print ecs_lines
    # print input_lines


    ##analysis ecs:
    inp = 0;
    ps_cpus, ps_mem, ps_hdd = (int(x) for x in input_lines[inp].split())
    # print ps_cpus, ps_mem, ps_hdd
    inp += 2
    flavors = int(input_lines[inp])
    # print flavors
    inp += 1
    types = []
    for i in xrange(flavors):
        tem = input_lines[inp + i].strip('\n').split()
        tem[1] = int(tem[1])
        tem[2] = int(tem[2]) / 1024
        # print tem
        types.append(tem)
    inp += flavors + 1
    target = input_lines[inp].strip('\n')
    inp += 2
    start_time = input_lines[inp].strip('\n')
    end_time = input_lines[inp + 1].strip('\n')
    # print start_time
    # print end_time

    ##analysis traindata
    typename = [x[0] for x in types]
    # print typename
    traindata = []
    traindata_count = []
    traindata_date = []
    tradate_begin = transdate((ecs_lines[0].split())[2])
    tradate_end = transdate((ecs_lines[len(ecs_lines) - 1].split())[2])
    vis_date = {}
    days = (tradate_end - tradate_begin).days
    now = {}
    nowdate = tradate_begin
    point = 0
    while nowdate <= tradate_end:
        # print nowdate
        tag = 0
        while True:
            if point >= len(ecs_lines):
                break
            x = ecs_lines[point]
            tem = x.split()
            # print tem
            time = transdate(tem[2])
            if time != nowdate:
                traindata_count.append(now)
                now = {}
                break
            tag = 1
            traindata.append(tem)
            if len(traindata_date) == 0 or traindata_date[len(traindata_date) - 1] != time:
                traindata_date.append(time)
                now[tem[1]] = 1
            else:
                if tem[1] not in now:
                    now[tem[1]] = 1
                else:
                    now[tem[1]] += 1
            point += 1
        if tag == 0:
            traindata_date.append(nowdate)
        nowdate = nowdate + datetime.timedelta(days=1)

    resu = []
    info_fla = []
    vm_num = 0
    lookback = 7
    st = transdate(start_time.split()[0])
    en = transdate(end_time.split()[0])
    window = (en - st).days
    print window
    for i in xrange(len(typename)):
        focus = typename[i]
        print focus
        focus_count = getdata(focus, traindata_count, days)
        oridata = [x for x in focus_count]
        scale = scaler()

        # print focus_count
        focus_count = scale.scale(focus_count)
        #print focus_count

        # print result
        predicted_knn = []
        predicted_trival = focus_count[days-window:days]
        for it in xrange(window):
            nextday = knn_predict(focus_count, lookback, 5)
            predicted_knn.append(nextday)
            focus_count.append(nextday)
        #predicted_knn = scale.recover(predicted_knn)
        #predicted_trival = scale.recover(predicted_trival)
        predicted = [predicted_knn[ip]*0.52 + predicted_trival[ip]*0.47 for ip in xrange(window)]
        predicted = scale.recover(predicted)
        print  predicted_knn
        inc = 0
        for it in xrange(window):
            inc += int(round(predicted[it]))

        print predicted_trival
        print predicted
        print inc
        # result = scale.recover(focus_count)
        ti_fla = types[i] + [inc]
        # print ti_fl
        info_fla.append(ti_fla)
        vm_num += inc
    et = datetime.datetime.now()
    info_phy = []
    info_phy.append(ps_cpus)
    info_phy.append(ps_mem)
    target = target.strip("\r")
    answer = []
    answer.append(str(vm_num))
    for i in xrange(len(info_fla)):
        #print info_fla[i][3]
        answer.append(info_fla[i][0] + ' ' + str(info_fla[i][3]))
    #print answer
    answer.append("")
    # print("vm_num:{0} , info_vm:{1}, info_phy: {2}, target:{3}").format(vm_num, info_fla, info_phy, target)
    # print info_fla
    # print str(pack(2, [['flavor5', 2, 4, 1], ['flavor4', 2, 2, 0], ['flavor3', 1, 4, 1], ['flavor2', 1, 2, 0],
    #                  ['flavor1', 1, 1, 0]], [56, 128], "CPU"))
    #answer += pack(vm_num, info_fla, info_phy, target)
    # print answer
    pack(vm_num, info_fla, info_phy, target, answer)
    return answer

