# libguestfs virt-v2v tool
# Copyright (C) 2009-2018 Red Hat Inc.
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.

include $(top_srcdir)/subdir-rules.mk

generator_built = \
	uefi.ml \
	uefi.mli

BUILT_SOURCES = \
	$(generator_built) \
	output_rhv_upload_createvm_source.ml \
	output_rhv_upload_plugin_source.ml \
	output_rhv_upload_precheck_source.ml

EXTRA_DIST = \
	$(SOURCES_MLI) $(SOURCES_ML) $(SOURCES_C) \
	copy_to_local.ml \
	copy_to_local.mli \
	embed.sh \
	rhv-upload-createvm.py \
	rhv-upload-plugin.py \
	rhv-upload-precheck.py \
	v2v_unit_tests.ml \
	virt-v2v.pod \
	virt-v2v-copy-to-local.pod \
	virt-v2v-input-vmware.pod \
	virt-v2v-input-xen.pod \
	virt-v2v-output-local.pod \
	virt-v2v-output-openstack.pod \
	virt-v2v-output-rhv.pod \
	virt-v2v-support.pod

SOURCES_MLI = \
	changeuid.mli \
	cmdline.mli \
	convert_linux.mli \
	convert_windows.mli \
	create_libvirt_xml.mli \
	create_ovf.mli \
	DOM.mli \
	input_disk.mli \
	input_libvirt.mli \
	input_libvirt_other.mli \
	input_libvirt_vcenter_https.mli \
	input_libvirt_vddk.mli \
	input_libvirt_xen_ssh.mli \
	input_libvirtxml.mli \
	input_ova.mli \
	input_vmx.mli \
	inspect_source.mli \
	libvirt_utils.mli \
	linux.mli \
	linux_bootloaders.mli \
	linux_kernels.mli \
	measure_disk.mli \
	modules_list.mli \
	name_from_disk.mli \
	networks.mli \
	openstack_image_properties.mli \
	output_glance.mli \
	output_libvirt.mli \
	output_local.mli \
	output_null.mli \
	output_openstack.mli \
	output_qemu.mli \
	output_rhv.mli \
	output_rhv_upload.mli \
	output_rhv_upload_createvm_source.mli \
	output_rhv_upload_plugin_source.mli \
	output_rhv_upload_precheck_source.mli \
	output_vdsm.mli \
	parse_ova.mli \
	parse_ovf_from_ova.mli \
	parse_libvirt_xml.mli \
	parse_vmx.mli \
	python_script.mli \
	qemuopts.mli \
	target_bus_assignment.mli \
	types.mli \
	uefi.mli \
	utils.mli \
	v2v.mli \
	vCenter.mli \
	windows.mli \
	windows_virtio.mli

SOURCES_ML = \
	types.ml \
	uefi.ml \
	utils.ml \
	python_script.ml \
	name_from_disk.ml \
	vCenter.ml \
	libvirt_utils.ml \
	DOM.ml \
	changeuid.ml \
	parse_ovf_from_ova.ml \
	parse_ova.ml \
	create_ovf.ml \
	linux.ml \
	windows.ml \
	windows_virtio.ml \
	modules_list.ml \
	input_disk.ml \
	parse_vmx.ml \
	parse_libvirt_xml.ml \
	create_libvirt_xml.ml \
	openstack_image_properties.ml \
	qemuopts.ml \
	input_libvirtxml.ml \
	input_libvirt_other.ml \
	input_libvirt_vcenter_https.ml \
	input_libvirt_vddk.ml \
	input_libvirt_xen_ssh.ml \
	input_libvirt.ml \
	input_ova.ml \
	input_vmx.ml \
	linux_bootloaders.ml \
	linux_kernels.ml \
	convert_linux.ml \
	convert_windows.ml \
	output_null.ml \
	output_glance.ml \
	output_libvirt.ml \
	output_local.ml \
	output_qemu.ml \
	output_rhv.ml \
	output_rhv_upload_createvm_source.ml \
	output_rhv_upload_plugin_source.ml \
	output_rhv_upload_precheck_source.ml \
	output_rhv_upload.ml \
	output_vdsm.ml \
	output_openstack.ml \
	inspect_source.ml \
	target_bus_assignment.ml \
	measure_disk.ml \
	networks.ml \
	cmdline.ml \
	v2v.ml

SOURCES_C = \
	libvirt_utils-c.c \
	qemuopts-c.c

# These files are generated and contain *.py embedded as an OCaml string.
output_rhv_upload_createvm_source.ml: $(srcdir)/rhv-upload-createvm.py
	$(srcdir)/embed.sh code $^ $@
output_rhv_upload_plugin_source.ml: $(srcdir)/rhv-upload-plugin.py
	$(srcdir)/embed.sh code $^ $@
output_rhv_upload_precheck_source.ml: $(srcdir)/rhv-upload-precheck.py
	$(srcdir)/embed.sh code $^ $@

if HAVE_OCAML

bin_PROGRAMS = virt-v2v virt-v2v-copy-to-local

virt_v2v_SOURCES = $(SOURCES_C)
virt_v2v_CPPFLAGS = \
	-I. \
	-I$(top_builddir) \
	-I$(shell $(OCAMLC) -where) \
	-I$(top_srcdir)/common/qemuopts \
	-I$(top_srcdir)/common/utils \
	-I$(top_srcdir)/lib
virt_v2v_CFLAGS = \
	$(WARN_CFLAGS) $(WERROR_CFLAGS) \
	$(LIBVIRT_CFLAGS)

BOBJECTS = \
	$(top_builddir)/customize/firstboot.cmo \
	$(top_builddir)/customize/SELinux_relabel.cmo \
	$(SOURCES_ML:.ml=.cmo)
XOBJECTS = $(BOBJECTS:.cmo=.cmx)

# -I $(top_builddir)/lib/.libs is a hack which forces corresponding -L
# option to be passed to gcc, so we don't try linking against an
# installed copy of libguestfs.
OCAMLPACKAGES = \
	-package str,unix \
	-I $(top_builddir)/common/utils/.libs \
	-I $(top_builddir)/common/qemuopts/.libs \
	-I $(top_builddir)/lib/.libs \
	-I $(top_builddir)/gnulib/lib/.libs \
	-I $(top_builddir)/ocaml \
	-I $(top_builddir)/common/mlstdutils \
	-I $(top_builddir)/common/mlutils \
	-I $(top_builddir)/common/mlgettext \
	-I $(top_builddir)/common/mlpcre \
	-I $(top_builddir)/common/mlxml \
	-I $(top_builddir)/common/mltools \
	-I $(top_builddir)/customize
if HAVE_OCAML_PKG_GETTEXT
OCAMLPACKAGES += -package gettext-stub
endif

OCAMLCLIBS = \
	-lutils \
	-lqemuopts \
	$(LIBVIRT_LIBS) \
	$(LIBXML2_LIBS) \
	$(JANSSON_LIBS) \
	$(LIBINTL) \
	-lgnu

OCAMLFLAGS = $(OCAML_FLAGS) $(OCAML_WARN_ERROR) -ccopt '$(CFLAGS)'

if !HAVE_OCAMLOPT
OBJECTS = $(BOBJECTS)
else
OBJECTS = $(XOBJECTS)
endif

OCAMLLINKFLAGS = \
	mlstdutils.$(MLARCHIVE) \
	mlguestfs.$(MLARCHIVE) \
	mlgettext.$(MLARCHIVE) \
	mlpcre.$(MLARCHIVE) \
	mlxml.$(MLARCHIVE) \
	mlcutils.$(MLARCHIVE) \
	mltools.$(MLARCHIVE) \
	$(LINK_CUSTOM_OCAMLC_ONLY)

virt_v2v_DEPENDENCIES = $(OBJECTS) $(top_srcdir)/ocaml-link.sh
virt_v2v_LINK = \
	$(top_srcdir)/ocaml-link.sh -cclib '$(OCAMLCLIBS)' -- \
	  $(OCAMLFIND) $(BEST) $(OCAMLFLAGS) $(OCAMLPACKAGES) $(OCAMLLINKFLAGS) \
	  $(OBJECTS) -o $@

virt_v2v_copy_to_local_SOURCES = \
	libvirt_utils-c.c
virt_v2v_copy_to_local_CPPFLAGS = \
	-I. \
	-I$(top_builddir) \
	-I$(shell $(OCAMLC) -where) \
	-I$(top_srcdir)/common/utils \
	-I$(top_srcdir)/lib
virt_v2v_copy_to_local_CFLAGS = \
	$(WARN_CFLAGS) $(WERROR_CFLAGS) \
	$(LIBVIRT_CFLAGS)

COPY_TO_LOCAL_BOBJECTS = \
	uefi.cmo \
	utils.cmo \
	libvirt_utils.cmo \
	vCenter.cmo \
	copy_to_local.cmo
COPY_TO_LOCAL_XOBJECTS = $(COPY_TO_LOCAL_BOBJECTS:.cmo=.cmx)

if !HAVE_OCAMLOPT
COPY_TO_LOCAL_OBJECTS = $(COPY_TO_LOCAL_BOBJECTS)
else
COPY_TO_LOCAL_OBJECTS = $(COPY_TO_LOCAL_XOBJECTS)
endif

virt_v2v_copy_to_local_DEPENDENCIES = \
	$(COPY_TO_LOCAL_OBJECTS) \
	../common/mlstdutils/mlstdutils.$(MLARCHIVE) \
	../common/mlxml/mlxml.$(MLARCHIVE) \
	../common/mlgettext/mlgettext.$(MLARCHIVE) \
	../common/mlpcre/mlpcre.$(MLARCHIVE) \
	../common/mlutils/mlcutils.$(MLARCHIVE) \
	../common/mltools/mltools.$(MLARCHIVE) \
	$(top_srcdir)/ocaml-link.sh
virt_v2v_copy_to_local_LINK = \
	$(top_srcdir)/ocaml-link.sh -cclib '$(OCAMLCLIBS)' -- \
	  $(OCAMLFIND) $(BEST) $(OCAMLFLAGS) $(OCAMLPACKAGES) $(OCAMLLINKFLAGS) \
	  $(COPY_TO_LOCAL_OBJECTS) -o $@

# Data directory.

virttoolsdatadir = $(datadir)/virt-tools

# Manual pages and HTML files for the website.

man_MANS = \
	virt-v2v.1 \
	virt-v2v-copy-to-local.1 \
	virt-v2v-input-vmware.1 \
	virt-v2v-input-xen.1 \
	virt-v2v-output-local.1 \
	virt-v2v-output-openstack.1 \
	virt-v2v-output-rhv.1 \
	virt-v2v-support.1

noinst_DATA = \
	$(top_builddir)/website/virt-v2v.1.html \
	$(top_builddir)/website/virt-v2v-copy-to-local.1.html \
	$(top_builddir)/website/virt-v2v-input-vmware.1.html \
	$(top_builddir)/website/virt-v2v-input-xen.1.html \
	$(top_builddir)/website/virt-v2v-output-local.1.html \
	$(top_builddir)/website/virt-v2v-output-openstack.1.html \
	$(top_builddir)/website/virt-v2v-output-rhv.1.html \
	$(top_builddir)/website/virt-v2v-support.1.html

virt-v2v.1 $(top_builddir)/website/virt-v2v.1.html: stamp-virt-v2v.pod

stamp-virt-v2v.pod: virt-v2v.pod
	$(PODWRAPPER) \
	  --man virt-v2v.1 \
	  --html $(top_builddir)/website/virt-v2v.1.html \
	  --license GPLv2+ \
	  --warning safe \
	  $<
	touch $@

virt-v2v-copy-to-local.1 $(top_builddir)/website/virt-v2v-copy-to-local.1.html: stamp-virt-v2v-copy-to-local.pod

stamp-virt-v2v-copy-to-local.pod: virt-v2v-copy-to-local.pod
	$(PODWRAPPER) \
	  --man virt-v2v-copy-to-local.1 \
	  --html $(top_builddir)/website/virt-v2v-copy-to-local.1.html \
	  --license GPLv2+ \
	  --warning safe \
	  $<
	touch $@

virt-v2v-input-vmware.1 $(top_builddir)/website/virt-v2v-input-vmware.1.html: stamp-virt-v2v-input-vmware.pod

stamp-virt-v2v-input-vmware.pod: virt-v2v-input-vmware.pod
	$(PODWRAPPER) \
	  --man virt-v2v-input-vmware.1 \
	  --html $(top_builddir)/website/virt-v2v-input-vmware.1.html \
	  --license GPLv2+ \
	  --warning safe \
	  $<
	touch $@

virt-v2v-input-xen.1 $(top_builddir)/website/virt-v2v-input-xen.1.html: stamp-virt-v2v-input-xen.pod

stamp-virt-v2v-input-xen.pod: virt-v2v-input-xen.pod
	$(PODWRAPPER) \
	  --man virt-v2v-input-xen.1 \
	  --html $(top_builddir)/website/virt-v2v-input-xen.1.html \
	  --license GPLv2+ \
	  --warning safe \
	  $<
	touch $@

virt-v2v-output-local.1 $(top_builddir)/website/virt-v2v-output-local.1.html: stamp-virt-v2v-output-local.pod

stamp-virt-v2v-output-local.pod: virt-v2v-output-local.pod
	$(PODWRAPPER) \
	  --man virt-v2v-output-local.1 \
	  --html $(top_builddir)/website/virt-v2v-output-local.1.html \
	  --license GPLv2+ \
	  --warning safe \
	  $<
	touch $@

virt-v2v-output-openstack.1 $(top_builddir)/website/virt-v2v-output-openstack.1.html: stamp-virt-v2v-output-openstack.pod

stamp-virt-v2v-output-openstack.pod: virt-v2v-output-openstack.pod
	$(PODWRAPPER) \
	  --man virt-v2v-output-openstack.1 \
	  --html $(top_builddir)/website/virt-v2v-output-openstack.1.html \
	  --license GPLv2+ \
	  --warning safe \
	  $<
	touch $@

virt-v2v-output-rhv.1 $(top_builddir)/website/virt-v2v-output-rhv.1.html: stamp-virt-v2v-output-rhv.pod

stamp-virt-v2v-output-rhv.pod: virt-v2v-output-rhv.pod
	$(PODWRAPPER) \
	  --man virt-v2v-output-rhv.1 \
	  --html $(top_builddir)/website/virt-v2v-output-rhv.1.html \
	  --license GPLv2+ \
	  --warning safe \
	  $<
	touch $@

virt-v2v-support.1 $(top_builddir)/website/virt-v2v-support.1.html: stamp-virt-v2v-support.pod

stamp-virt-v2v-support.pod: virt-v2v-support.pod
	$(PODWRAPPER) \
	  --man virt-v2v-support.1 \
	  --html $(top_builddir)/website/virt-v2v-support.1.html \
	  --license GPLv2+ \
	  --warning safe \
	  $<
	touch $@

# Tests.

# The virt-v2v tests here are not meant to be thorough tests of guest
# conversion.  There is a test suite used to test conversion which is
# kept outside libguestfs because it contains lots of proprietary
# unredistributable guests like Windows.
#
# The tests here instead are testing:
#
# - virt-v2v command line arguments
# - virt-v2v reads and writes files to the correct places
# - valgrind & memory leaks
# - any conversion properties that can be tested using just the
#   phony guests (but we don't go out of our way here)
# - that up to date guests don't crash virt-v2v

TESTS_ENVIRONMENT = $(top_builddir)/run --test

TESTS = \
	test-v2v-docs.sh \
	test-v2v-python-syntax.sh \
	test-v2v-i-ova-bad-sha1.sh \
	test-v2v-i-ova-bad-sha256.sh \
	test-v2v-i-ova-formats.sh \
	test-v2v-i-ova-good-checksums.sh \
	test-v2v-i-ova-gz.sh \
	test-v2v-i-ova-invalid-manifest1.sh \
	test-v2v-i-ova-invalid-manifest2.sh \
	test-v2v-i-ova-snapshots.sh \
	test-v2v-i-ova-subfolders.sh \
	test-v2v-i-ova-tar.sh \
	test-v2v-i-ova-two-disks.sh \
	test-v2v-i-vmx.sh \
	test-v2v-it-vddk-io-query.sh \
	test-v2v-o-rhv-upload-oo-query.sh \
	test-v2v-o-vdsm-oo-query.sh \
	test-v2v-bad-networks-and-bridges.sh

if HAVE_LIBVIRT
TESTS += \
	test-v2v-copy-to-local.sh
endif

if HAVE_OCAML_PKG_OUNIT
TESTS += v2v_unit_tests
endif

if ENABLE_APPLIANCE
TESTS += \
	test-v2v-i-ova.sh \
	test-v2v-i-disk.sh \
	test-v2v-machine-readable.sh \
	test-v2v-virtio-win-iso.sh \
	test-v2v-windows-conversion.sh

if HAVE_LIBVIRT
TESTS += \
	test-v2v-cdrom.sh \
	test-v2v-floppy.sh \
	test-v2v-in-place.sh \
	test-v2v-mac.sh \
	test-v2v-networks-and-bridges.sh \
	test-v2v-no-copy.sh \
	test-v2v-o-glance.sh \
	test-v2v-o-libvirt.sh \
	test-v2v-o-null.sh \
	test-v2v-o-openstack.sh \
	test-v2v-o-qemu.sh \
	test-v2v-o-rhv.sh \
	test-v2v-o-rhv-upload.sh \
	test-v2v-o-vdsm-options.sh \
	test-v2v-oa-option.sh \
	test-v2v-of-option.sh \
	test-v2v-on-option.sh \
	test-v2v-print-estimate.sh \
	test-v2v-print-source.sh \
	test-v2v-sound.sh \
	$(SLOW_TESTS) \
	$(ROOT_TESTS)
endif
endif ENABLE_APPLIANCE

# The VMDK file is used for some -i ova tests.
check_DATA = windows.vmdk
if ENABLE_APPLIANCE
windows.vmdk: ../test-data/phony-guests/windows.img
	rm -f $@ $@-t
	if [ -s $< ]; then \
	    qemu-img convert -f raw $< -O vmdk $@-t; \
	    mv $@-t $@; \
	else \
	    touch $@; \
	fi
else
windows.vmdk:
	touch $@
endif

DISTCLEANFILES += \
	windows.vmdk

check-valgrind:
	$(MAKE) VG="@VG@" check

SLOW_TESTS = \
	$(real_guests_scripts) \
	test-v2v-trim.sh

check-slow:
	$(MAKE) check TESTS="$(SLOW_TESTS)" SLOW=1

ROOT_TESTS = \
	test-v2v-i-ova-as-root.sh

check-root:
	$(MAKE) check TESTS="$(ROOT_TESTS)"

# A selection of real guests that test-v2v-conversion-of.sh will
# try to convert.  This is only used by 'make check-slow'.

real_guests_scripts = \
	test-v2v-conversion-of-centos-6.sh \
	test-v2v-conversion-of-centos-7.0.sh \
	test-v2v-conversion-of-debian-6.sh \
	test-v2v-conversion-of-debian-7.sh \
	test-v2v-conversion-of-debian-8.sh \
	test-v2v-conversion-of-fedora-20.sh \
	test-v2v-conversion-of-fedora-23.sh \
	test-v2v-conversion-of-opensuse-13.1.sh \
	test-v2v-conversion-of-opensuse-13.2.sh \
	test-v2v-conversion-of-opensuse-42.1.sh \
	test-v2v-conversion-of-rhel-5.10.sh \
	test-v2v-conversion-of-rhel-6.8.sh \
	test-v2v-conversion-of-rhel-7.0.sh \
	test-v2v-conversion-of-rhel-7.2.sh \
	test-v2v-conversion-of-ubuntu-10.04.sh \
	test-v2v-conversion-of-ubuntu-12.04.sh \
	test-v2v-conversion-of-ubuntu-14.04.sh \
	test-v2v-conversion-of-ubuntu-16.04.sh \
	test-v2v-conversion-of-ubuntu-18.04.sh \
	test-v2v-conversion-of-windows-6.2-server.sh \
	test-v2v-conversion-of-windows-6.3-server.sh \
	test-v2v-conversion-of-windows-10.0-server.sh

test-v2v-conversion-of-%.sh:
	rm -f $@ $@-t
	f=`echo "$@" | $(SED) 's/test-v2v-conversion-of-\(.*\).sh/\1/'`; \
	echo 'script=$@ exec $$srcdir/test-v2v-conversion-of.sh' "$$f" > $@-t
	chmod 0755 $@-t
	mv $@-t $@

CLEANFILES += \
	$(real_guests_scripts) \
	real-*.img \
	real-*.xml

EXTRA_DIST += \
	test-v2v-bad-networks-and-bridges.sh \
	test-v2v-cdrom.expected \
	test-v2v-cdrom.sh \
	test-v2v-cdrom.xml \
	test-v2v-copy-to-local.sh \
	test-v2v-docs.sh \
	test-v2v-floppy.expected \
	test-v2v-floppy.sh \
	test-v2v-floppy.xml \
	test-v2v-i-disk.sh \
	test-v2v-i-ova-as-root.ovf \
	test-v2v-i-ova-as-root.sh \
	test-v2v-i-ova-bad-sha1.sh \
	test-v2v-i-ova-bad-sha256.sh \
	test-v2v-i-ova-checksums.ovf \
	test-v2v-i-ova-formats.expected \
	test-v2v-i-ova-formats.ovf \
	test-v2v-i-ova-formats.sh \
	test-v2v-i-ova-good-checksums.sh \
	test-v2v-i-ova-gz.expected \
	test-v2v-i-ova-gz.ovf \
	test-v2v-i-ova-gz.sh \
	test-v2v-i-ova-invalid-manifest1.sh \
	test-v2v-i-ova-invalid-manifest2.sh \
	test-v2v-i-ova-snapshots.expected \
	test-v2v-i-ova-snapshots.expected2 \
	test-v2v-i-ova-snapshots.ovf \
	test-v2v-i-ova-snapshots.sh \
	test-v2v-i-ova-subfolders.expected \
	test-v2v-i-ova-subfolders.expected2 \
	test-v2v-i-ova-subfolders.ovf \
	test-v2v-i-ova-subfolders.sh \
	test-v2v-i-ova-tar.expected \
	test-v2v-i-ova-tar.expected2 \
	test-v2v-i-ova-tar.ovf \
	test-v2v-i-ova-tar.sh \
	test-v2v-i-ova-two-disks.expected \
	test-v2v-i-ova-two-disks.expected2 \
	test-v2v-i-ova-two-disks.ovf \
	test-v2v-i-ova-two-disks.sh \
	test-v2v-i-ova.ovf \
	test-v2v-i-ova.sh \
	test-v2v-i-ova.xml \
	test-v2v-i-vmx.sh \
	test-v2v-i-vmx-1.expected \
	test-v2v-i-vmx-2.expected \
	test-v2v-i-vmx-3.expected \
	test-v2v-i-vmx-4.expected \
	test-v2v-i-vmx-5.expected \
	test-v2v-i-vmx-1.vmx \
	test-v2v-i-vmx-2.vmx \
	test-v2v-i-vmx-3.vmx \
	test-v2v-i-vmx-4.vmx \
	test-v2v-i-vmx-5.vmx \
	test-v2v-in-place.sh \
	test-v2v-it-vddk-io-query.sh \
	test-v2v-machine-readable.sh \
	test-v2v-mac-expected.xml \
	test-v2v-mac.sh \
	test-v2v-mac.xml \
	test-v2v-networks-and-bridges-expected.xml \
	test-v2v-networks-and-bridges.sh \
	test-v2v-networks-and-bridges.xml \
	test-v2v-no-copy.sh \
	test-v2v-o-glance.sh \
	test-v2v-o-libvirt.sh \
	test-v2v-o-null.sh \
	test-v2v-o-openstack.sh \
	test-v2v-o-qemu.sh \
	test-v2v-o-rhv.ovf.expected \
	test-v2v-o-rhv.sh \
	test-v2v-o-rhv-upload.sh \
	test-v2v-o-rhv-upload-module/ovirtsdk4/__init__.py \
	test-v2v-o-rhv-upload-module/ovirtsdk4/types.py \
	test-v2v-o-rhv-upload-oo-query.sh \
	test-v2v-o-vdsm-oo-query.sh \
	test-v2v-o-vdsm-options.ovf.expected \
	test-v2v-o-vdsm-options.sh \
	test-v2v-oa-option.sh \
	test-v2v-of-option.sh \
	test-v2v-on-option.sh \
	test-v2v-print-estimate.sh \
	test-v2v-print-source.expected \
	test-v2v-print-source.sh \
	test-v2v-print-source.xml \
	test-v2v-python-syntax.sh \
	test-v2v-conversion-of.sh \
	test-v2v-sound.sh \
	test-v2v-sound.xml \
	test-v2v-trim.sh \
	test-v2v-virtio-win-iso.sh \
	test-v2v-windows-conversion.sh

# Unit tests.
check_PROGRAMS =
if HAVE_OCAML_PKG_OUNIT
check_PROGRAMS += v2v_unit_tests
endif

v2v_unit_tests_BOBJECTS = \
	types.cmo \
	uefi.cmo \
	utils.cmo \
	DOM.cmo \
	create_ovf.cmo \
	windows.cmo \
	linux.cmo \
	windows_virtio.cmo \
	parse_vmx.cmo \
	v2v_unit_tests.cmo
v2v_unit_tests_XOBJECTS = $(v2v_unit_tests_BOBJECTS:.cmo=.cmx)

v2v_unit_tests_SOURCES = $(virt_v2v_SOURCES)
v2v_unit_tests_CPPFLAGS = $(virt_v2v_CPPFLAGS)
v2v_unit_tests_CFLAGS = $(virt_v2v_CFLAGS)

if !HAVE_OCAMLOPT
# Can't call this v2v_unit_tests_OBJECTS because automake gets confused.
v2v_unit_tests_THEOBJECTS = $(v2v_unit_tests_BOBJECTS)
v2v_unit_tests.cmo: OCAMLPACKAGES += -package oUnit
else
v2v_unit_tests_THEOBJECTS = $(v2v_unit_tests_XOBJECTS)
v2v_unit_tests.cmx: OCAMLPACKAGES += -package oUnit
endif

v2v_unit_tests_DEPENDENCIES = \
	$(v2v_unit_tests_THEOBJECTS) \
	../common/mlstdutils/mlstdutils.$(MLARCHIVE) \
	../common/mlxml/mlxml.$(MLARCHIVE) \
	../common/mlgettext/mlgettext.$(MLARCHIVE) \
	../common/mlpcre/mlpcre.$(MLARCHIVE) \
	../common/mlutils/mlcutils.$(MLARCHIVE) \
	../common/mltools/mltools.$(MLARCHIVE) \
	$(top_srcdir)/ocaml-link.sh
v2v_unit_tests_LINK = \
	$(top_srcdir)/ocaml-link.sh -cclib '$(OCAMLCLIBS)' -- \
	  $(OCAMLFIND) $(BEST) $(OCAMLFLAGS) \
	  $(OCAMLPACKAGES) -package oUnit \
	  $(OCAMLLINKFLAGS) \
	  $(v2v_unit_tests_THEOBJECTS) -o $@

# Dependencies.
.depend: \
	$(srcdir)/*.mli \
	$(srcdir)/*.ml \
	output_rhv_upload_*_source.ml
	$(top_builddir)/ocaml-dep.sh $^
-include .depend

endif

.PHONY: docs
