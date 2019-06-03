# not a GNU package. You can remove this line, if
# have all needed files, that a GNU package needs
AUTOMAKE_OPTIONS = foreign 1.4
ACLOCAL_AMFLAGS = -I m4
EXTRA_DIST = ChangeLog COPYING LICENSE suricata.yaml.in \
             classification.config threshold.config \
             reference.config $(SURICATA_UPDATE_DIR) \
	     lua
SUBDIRS = $(HTP_DIR) rust src qa rules doc contrib etc python ebpf \
          $(SURICATA_UPDATE_DIR)

CLEANFILES = stamp-h[0-9]*

install-data-am:
	@echo "Run 'make install-conf' if you want to install initial configuration files. Or 'make install-full' to install configuration and rules";

install-full:
	$(MAKE) install
	$(MAKE) install-conf
	$(MAKE) install-rules

install-conf:
	install -d "$(DESTDIR)$(e_sysconfdir)"
	@test -e "$(DESTDIR)$(e_sysconfdir)/suricata.yaml" || install -m 600 "$(top_srcdir)/suricata.yaml" "$(DESTDIR)$(e_sysconfdir)"
	@test -e "$(DESTDIR)$(e_sysconfdir)/classification.config" || install -m 600 "$(top_srcdir)/classification.config" "$(DESTDIR)$(e_sysconfdir)"
	@test -e "$(DESTDIR)$(e_sysconfdir)/reference.config" || install -m 600 "$(top_srcdir)/reference.config" "$(DESTDIR)$(e_sysconfdir)"
	@test -e "$(DESTDIR)$(e_sysconfdir)/threshold.config" || install -m 600 "$(top_srcdir)/threshold.config" "$(DESTDIR)$(e_sysconfdir)"
	install -d "$(DESTDIR)$(e_logfilesdir)"
	install -d "$(DESTDIR)$(e_logcertsdir)"
	install -d "$(DESTDIR)$(e_rundir)"
	install -m 770 -d "$(DESTDIR)$(e_localstatedir)"

install-rules:
if HAVE_SURICATA_UPDATE
	$(DESTDIR)$(bindir)/suricata-update \
		--suricata $(DESTDIR)$(bindir)/suricata \
		--suricata-conf $(DESTDIR)$(sysconfdir)/suricata/suricata.yaml \
		--no-test --no-reload
else
	echo "error: rules not installed as suricata-update not available"
	exit 1
endif
	@test -e "$(DESTDIR)$(e_sysconfrulesdir)decoder-events.rules" || install -m 600 "$(top_srcdir)/rules/decoder-events.rules" "$(DESTDIR)$(e_sysconfrulesdir)"
	@test -e "$(DESTDIR)$(e_sysconfrulesdir)stream-events.rules" || install -m 600 "$(top_srcdir)/rules/stream-events.rules" "$(DESTDIR)$(e_sysconfrulesdir)"
	@test -e "$(DESTDIR)$(e_sysconfrulesdir)smtp-events.rules" || install -m 600 "$(top_srcdir)/rules/smtp-events.rules" "$(DESTDIR)$(e_sysconfrulesdir)"
	@test -e "$(DESTDIR)$(e_sysconfrulesdir)http-events.rules" || install -m 600 "$(top_srcdir)/rules/http-events.rules" "$(DESTDIR)$(e_sysconfrulesdir)"
	@test -e "$(DESTDIR)$(e_sysconfrulesdir)dns-events.rules" || install -m 600 "$(top_srcdir)/rules/dns-events.rules" "$(DESTDIR)$(e_sysconfrulesdir)"
	@test -e "$(DESTDIR)$(e_sysconfrulesdir)tls-events.rules" || install -m 600 "$(top_srcdir)/rules/tls-events.rules" "$(DESTDIR)$(e_sysconfrulesdir)"
	@test -e "$(DESTDIR)$(e_sysconfrulesdir)modbus-events.rules" || install -m 600 "$(top_srcdir)/rules/modbus-events.rules" "$(DESTDIR)$(e_sysconfrulesdir)"
	@test -e "$(DESTDIR)$(e_sysconfrulesdir)app-layer-events.rules" || install -m 600 "$(top_srcdir)/rules/app-layer-events.rules" "$(DESTDIR)$(e_sysconfrulesdir)"
	@test -e "$(DESTDIR)$(e_sysconfrulesdir)dnp3-events.rules" || install -m 600 "$(top_srcdir)/rules/dnp3-events.rules" "$(DESTDIR)$(e_sysconfrulesdir)"
	@test -e "$(DESTDIR)$(e_sysconfrulesdir)dhcp-events.rules" || install -m 600 "$(top_srcdir)/rules/dhcp-events.rules" "$(DESTDIR)$(e_sysconfrulesdir)"
	@test -e "$(DESTDIR)$(e_sysconfrulesdir)ipsec-events.rules" || install -m 600 "$(top_srcdir)/rules/ipsec-events.rules" "$(DESTDIR)$(e_sysconfrulesdir)"
	@test -e "$(DESTDIR)$(e_sysconfrulesdir)kerberos-events.rules" || install -m 600 "$(top_srcdir)/rules/kerberos-events.rules" "$(DESTDIR)$(e_sysconfrulesdir)"
	@test -e "$(DESTDIR)$(e_sysconfrulesdir)nfs-events.rules" || install -m 600 "$(top_srcdir)/rules/nfs-events.rules" "$(DESTDIR)$(e_sysconfrulesdir)"
	@test -e "$(DESTDIR)$(e_sysconfrulesdir)ntp-events.rules" || install -m 600 "$(top_srcdir)/rules/ntp-events.rules" "$(DESTDIR)$(e_sysconfrulesdir)"
	@test -e "$(DESTDIR)$(e_sysconfrulesdir)smb-events.rules" || install -m 600 "$(top_srcdir)/rules/smb-events.rules" "$(DESTDIR)$(e_sysconfrulesdir)"
	@echo ""
	@echo "You can now start suricata by running as root something like:"
	@echo "  $(DESTDIR)$(bindir)/suricata -c $(DESTDIR)$(e_sysconfdir)suricata.yaml -i eth0"
	@echo ""
	@echo "If a library like libhtp.so is not found, you can run suricata with:"
	@echo "  LD_LIBRARY_PATH="$(DESTDIR)$(prefix)/lib" "$(DESTDIR)$(bindir)/suricata" -c "$(DESTDIR)$(e_sysconfdir)suricata.yaml" -i eth0"
	@echo ""
	@echo "The Emerging Threats Open rules are now installed. Rules can be"
	@echo "updated and managed with the suricata-update tool."
	@echo ""
	@echo "For more information please see:"
	@echo "  https://suricata.readthedocs.io/en/latest/rule-management/index.html"
	@echo ""
