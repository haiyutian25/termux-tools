# Copyright (C) 2022 Termux

# This file is part of termux-tools.

# termux-tools is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.

# termux-tools is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with termux-tools.  If not, see
# <https://www.gnu.org/licenses/>.


# We have two variants of our motd message loaded by login script:
#   1. motd.sh: A dynamic motd that is executed with bash and echos a
#      motd message with escape sequences, optionally with a terminal logo.
#   2. motd: A static motd that is just read as is with cat and displayed.

sysconf_DATA = motd.sh motd

CLEANFILES = motd.sh motd


do_subst = sed -e "s%[@]TERMUX_PREFIX[@]%$(termux_prefix)%g"

define process-rule
$1: $1.in Makefile
	@echo "Creating $1"
	@$$(do_subst) < $(srcdir)/$1.in > $1
endef

$(eval $(call process-rule,motd.sh))


motd:
	@echo "Creating motd file"

	@echo "Termux 版本：${TERMUX_VERSION}" > motd
	@echo "" >> motd
	@echo "软件包管理：" >> motd
	@echo "" >> motd
	@echo " - 搜索：  pkg search <查询>" >> motd
	@echo " - 安装：  pkg install <软件包>" >> motd
	@echo " - 升级：  pkg upgrade" >> motd

    ifeq ($(TERMUX_PACKAGE_MANAGER),apt)
		@echo "" >> motd
		@echo "订阅额外的软件仓库：" >> motd
		@echo "" >> motd
		@echo " - Root：   pkg install root-repo" >> motd
		@echo " - X11：    pkg install x11-repo" >> motd
		@echo "" >> motd
		@echo "如需修复软件仓库问题，" >> motd
		@echo "请尝试 'termux-change-repo' 命令。" >> motd
    endif
