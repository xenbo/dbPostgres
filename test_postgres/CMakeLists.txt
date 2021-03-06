cmake_minimum_required(VERSION 3.10)
project(test_postgres C)

set(CMAKE_C_STANDARD 99)

add_definitions("-Wall -Wmissing-prototypes -Wpointer-arith -Wdeclaration-after-statement -Wendif-labels -Wmissing-format-attribute -Wformat-security -fno-strict-aliasing -fwrapv -fexcess-precision=standard -g")
add_definitions(-D_GNU_SOURCE)
add_definitions(-DDLSUFFIX='.so')


#include_directories(/home/dongbo/Desktop/postgresql-10.4/src/include)
include_directories(include)
link_directories(/home/dongbo/Desktop/postgresql-10.4/lib)

FILE(GLOB pgbackend_src
        "access/brin/brin.c"
        "access/brin/brin_pageops.c"
        "access/brin/brin_revmap.c"
        "access/brin/brin_tuple.c"
        "access/brin/brin_xlog.c"
        "access/brin/brin_minmax.c"
        "access/brin/brin_inclusion.c"
        "access/brin/brin_validate.c"
        "access/common/bufmask.c"
        "access/common/heaptuple.c"
        "access/common/indextuple.c"
        "access/common/printsimple.c"
        "access/common/printtup.c"
        "access/common/reloptions.c"
        "access/common/scankey.c"
        "access/common/tupconvert.c"
        "access/common/tupdesc.c"
        "access/gin/ginutil.c"
        "access/gin/gininsert.c"
        "access/gin/ginxlog.c"
        "access/gin/ginentrypage.c"
        "access/gin/gindatapage.c"
        "access/gin/ginbtree.c"
        "access/gin/ginscan.c"
        "access/gin/ginget.c"
        "access/gin/ginvacuum.c"
        "access/gin/ginarrayproc.c"
        "access/gin/ginbulk.c"
        "access/gin/ginfast.c"
        "access/gin/ginpostinglist.c"
        "access/gin/ginlogic.c"
        "access/gin/ginvalidate.c"
        "access/gist/gist.c"
        "access/gist/gistutil.c"
        "access/gist/gistxlog.c"
        "access/gist/gistvacuum.c"
        "access/gist/gistget.c"
        "access/gist/gistscan.c"
        "access/gist/gistproc.c"
        "access/gist/gistsplit.c"
        "access/gist/gistbuild.c"
        "access/gist/gistbuildbuffers.c"
        "access/gist/gistvalidate.c"
        "access/hash/hash.c"
        "access/hash/hashfunc.c"
        "access/hash/hashinsert.c"
        "access/hash/hashovfl.c"
        "access/hash/hashpage.c"
        "access/hash/hashsearch.c"
        "access/hash/hashsort.c"
        "access/hash/hashutil.c"
        "access/hash/hashvalidate.c"
        "access/hash/hash_xlog.c"
        "access/heap/heapam.c"
        "access/heap/hio.c"
        "access/heap/pruneheap.c"
        "access/heap/rewriteheap.c"
        "access/heap/syncscan.c"
        "access/heap/tuptoaster.c"
        "access/heap/visibilitymap.c"
        "access/index/amapi.c"
        "access/index/amvalidate.c"
        "access/index/genam.c"
        "access/index/indexam.c"
        "access/nbtree/nbtcompare.c"
        "access/nbtree/nbtinsert.c"
        "access/nbtree/nbtpage.c"
        "access/nbtree/nbtree.c"
        "access/nbtree/nbtsearch.c"
        "access/nbtree/nbtutils.c"
        "access/nbtree/nbtsort.c"
        "access/nbtree/nbtvalidate.c"
        "access/nbtree/nbtxlog.c"
        "access/rmgrdesc/brindesc.c"
        "access/rmgrdesc/clogdesc.c"
        "access/rmgrdesc/committsdesc.c"
        "access/rmgrdesc/dbasedesc.c"
        "access/rmgrdesc/genericdesc.c"
        "access/rmgrdesc/gindesc.c"
        "access/rmgrdesc/gistdesc.c"
        "access/rmgrdesc/hashdesc.c"
        "access/rmgrdesc/heapdesc.c"
        "access/rmgrdesc/logicalmsgdesc.c"
        "access/rmgrdesc/mxactdesc.c"
        "access/rmgrdesc/nbtdesc.c"
        "access/rmgrdesc/relmapdesc.c"
        "access/rmgrdesc/replorigindesc.c"
        "access/rmgrdesc/seqdesc.c"
        "access/rmgrdesc/smgrdesc.c"
        "access/rmgrdesc/spgdesc.c"
        "access/rmgrdesc/standbydesc.c"
        "access/rmgrdesc/tblspcdesc.c"
        "access/rmgrdesc/xactdesc.c"
        "access/rmgrdesc/xlogdesc.c"
        "access/spgist/spgutils.c"
        "access/spgist/spginsert.c"
        "access/spgist/spgscan.c"
        "access/spgist/spgvacuum.c"
        "access/spgist/spgvalidate.c"
        "access/spgist/spgdoinsert.c"
        "access/spgist/spgxlog.c"
        "access/spgist/spgtextproc.c"
        "access/spgist/spgquadtreeproc.c"
        "access/spgist/spgkdtreeproc.c"
        "access/tablesample/bernoulli.c"
        "access/tablesample/system.c"
        "access/tablesample/tablesample.c"
        "access/transam/clog.c"
        "access/transam/commit_ts.c"
        "access/transam/generic_xlog.c"
        "access/transam/multixact.c"
        "access/transam/parallel.c"
        "access/transam/rmgr.c"
        "access/transam/slru.c"
        "access/transam/subtrans.c"
        "access/transam/timeline.c"
        "access/transam/transam.c"
        "access/transam/twophase.c"
        "access/transam/twophase_rmgr.c"
        "access/transam/varsup.c"
        "access/transam/xact.c"
        "access/transam/xlog.c"
        "access/transam/xlogarchive.c"
        "access/transam/xlogfuncs.c"
        "access/transam/xloginsert.c"
        "access/transam/xlogreader.c"
        "access/transam/xlogutils.c"
        "bootstrap/bootparse.c"
        "bootstrap/bootstrap.c"
        "catalog/catalog.c"
        "catalog/dependency.c"
        "catalog/heap.c"
        "catalog/index.c"
        "catalog/indexing.c"
        "catalog/namespace.c"
        "catalog/aclchk.c"
        "catalog/objectaccess.c"
        "catalog/objectaddress.c"
        "catalog/partition.c"
        "catalog/pg_aggregate.c"
        "catalog/pg_collation.c"
        "catalog/pg_constraint.c"
        "catalog/pg_conversion.c"
        "catalog/pg_depend.c"
        "catalog/pg_enum.c"
        "catalog/pg_inherits.c"
        "catalog/pg_largeobject.c"
        "catalog/pg_namespace.c"
        "catalog/pg_operator.c"
        "catalog/pg_proc.c"
        "catalog/pg_publication.c"
        "catalog/pg_range.c"
        "catalog/pg_db_role_setting.c"
        "catalog/pg_shdepend.c"
        "catalog/pg_subscription.c"
        "catalog/pg_type.c"
        "catalog/storage.c"
        "catalog/toasting.c"
        "parser/analyze.c"
        "parser/gram.c"
        "parser/scan.c"
        "parser/parser.c"
        "parser/parse_agg.c"
        "parser/parse_clause.c"
        "parser/parse_coerce.c"
        "parser/parse_collate.c"
        "parser/parse_cte.c"
        "parser/parse_enr.c"
        "parser/parse_expr.c"
        "parser/parse_func.c"
        "parser/parse_node.c"
        "parser/parse_oper.c"
        "parser/parse_param.c"
        "parser/parse_relation.c"
        "parser/parse_target.c"
        "parser/parse_type.c"
        "parser/parse_utilcmd.c"
        "parser/scansup.c"
        "commands/amcmds.c"
        "commands/aggregatecmds.c"
        "commands/alter.c"
        "commands/analyze.c"
        "commands/async.c"
        "commands/cluster.c"
        "commands/comment.c"
        "commands/collationcmds.c"
        "commands/constraint.c"
        "commands/conversioncmds.c"
        "commands/copy.c"
        "commands/createas.c"
        "commands/dbcommands.c"
        "commands/define.c"
        "commands/discard.c"
        "commands/dropcmds.c"
        "commands/event_trigger.c"
        "commands/explain.c"
        "commands/extension.c"
        "commands/foreigncmds.c"
        "commands/functioncmds.c"
        "commands/indexcmds.c"
        "commands/lockcmds.c"
        "commands/matview.c"
        "commands/operatorcmds.c"
        "commands/opclasscmds.c"
        "commands/policy.c"
        "commands/portalcmds.c"
        "commands/prepare.c"
        "commands/proclang.c"
        "commands/publicationcmds.c"
        "commands/schemacmds.c"
        "commands/seclabel.c"
        "commands/sequence.c"
        "commands/statscmds.c"
        "commands/subscriptioncmds.c"
        "commands/tablecmds.c"
        "commands/tablespace.c"
        "commands/trigger.c"
        "commands/tsearchcmds.c"
        "commands/typecmds.c"
        "commands/user.c"
        "commands/vacuum.c"
        "commands/vacuumlazy.c"
        "commands/variable.c"
        "commands/view.c"
        "executor/execAmi.c"
        "executor/execCurrent.c"
        "executor/execExpr.c"
        "executor/execExprInterp.c"
        "executor/execGrouping.c"
        "executor/execIndexing.c"
        "executor/execJunk.c"
        "executor/execMain.c"
        "executor/execParallel.c"
        "executor/execProcnode.c"
        "executor/execReplication.c"
        "executor/execScan.c"
        "executor/execSRF.c"
        "executor/execTuples.c"
        "executor/execUtils.c"
        "executor/functions.c"
        "executor/instrument.c"
        "executor/nodeAppend.c"
        "executor/nodeAgg.c"
        "executor/nodeBitmapAnd.c"
        "executor/nodeBitmapOr.c"
        "executor/nodeBitmapHeapscan.c"
        "executor/nodeBitmapIndexscan.c"
        "executor/nodeCustom.c"
        "executor/nodeFunctionscan.c"
        "executor/nodeGather.c"
        "executor/nodeHash.c"
        "executor/nodeHashjoin.c"
        "executor/nodeIndexscan.c"
        "executor/nodeIndexonlyscan.c"
        "executor/nodeLimit.c"
        "executor/nodeLockRows.c"
        "executor/nodeGatherMerge.c"
        "executor/nodeMaterial.c"
        "executor/nodeMergeAppend.c"
        "executor/nodeMergejoin.c"
        "executor/nodeModifyTable.c"
        "executor/nodeNestloop.c"
        "executor/nodeProjectSet.c"
        "executor/nodeRecursiveunion.c"
        "executor/nodeResult.c"
        "executor/nodeSamplescan.c"
        "executor/nodeSeqscan.c"
        "executor/nodeSetOp.c"
        "executor/nodeSort.c"
        "executor/nodeUnique.c"
        "executor/nodeValuesscan.c"
        "executor/nodeCtescan.c"
        "executor/nodeNamedtuplestorescan.c"
        "executor/nodeWorktablescan.c"
        "executor/nodeGroup.c"
        "executor/nodeSubplan.c"
        "executor/nodeSubqueryscan.c"
        "executor/nodeTidscan.c"
        "executor/nodeForeignscan.c"
        "executor/nodeWindowAgg.c"
        "executor/tstoreReceiver.c"
        "executor/tqueue.c"
        "executor/spi.c"
        "executor/nodeTableFuncscan.c"
        "foreign/foreign.c"
        "lib/binaryheap.c"
        "lib/bipartite_match.c"
        "lib/hyperloglog.c"
        "lib/ilist.c"
        "lib/knapsack.c"
        "lib/pairingheap.c"
        "lib/rbtree.c"
        "lib/stringinfo.c"
        "libpq/be-fsstubs.c"
        "libpq/be-secure.c"
        "libpq/auth.c"
        "libpq/crypt.c"
        "libpq/hba.c"
        "libpq/ifaddr.c"
        "libpq/pqcomm.c"
        "libpq/pqformat.c"
        "libpq/pqmq.c"
        "libpq/pqsignal.c"
        "libpq/auth-scram.c"
        "main/main.c"
        "nodes/nodeFuncs.c"
        "nodes/nodes.c"
        "nodes/list.c"
        "nodes/bitmapset.c"
        "nodes/tidbitmap.c"
        "nodes/copyfuncs.c"
        "nodes/equalfuncs.c"
        "nodes/extensible.c"
        "nodes/makefuncs.c"
        "nodes/outfuncs.c"
        "nodes/readfuncs.c"
        "nodes/print.c"
        "nodes/read.c"
        "nodes/params.c"
        "nodes/value.c"
        "optimizer/geqo/geqo_copy.c"
        "optimizer/geqo/geqo_eval.c"
        "optimizer/geqo/geqo_main.c"
        "optimizer/geqo/geqo_misc.c"
        "optimizer/geqo/geqo_mutation.c"
        "optimizer/geqo/geqo_pool.c"
        "optimizer/geqo/geqo_random.c"
        "optimizer/geqo/geqo_recombination.c"
        "optimizer/geqo/geqo_selection.c"
        "optimizer/geqo/geqo_erx.c"
        "optimizer/geqo/geqo_pmx.c"
        "optimizer/geqo/geqo_cx.c"
        "optimizer/geqo/geqo_px.c"
        "optimizer/geqo/geqo_ox1.c"
        "optimizer/geqo/geqo_ox2.c"
        "optimizer/path/allpaths.c"
        "optimizer/path/clausesel.c"
        "optimizer/path/costsize.c"
        "optimizer/path/equivclass.c"
        "optimizer/path/indxpath.c"
        "optimizer/path/joinpath.c"
        "optimizer/path/joinrels.c"
        "optimizer/path/pathkeys.c"
        "optimizer/path/tidpath.c"
        "optimizer/plan/analyzejoins.c"
        "optimizer/plan/createplan.c"
        "optimizer/plan/initsplan.c"
        "optimizer/plan/planagg.c"
        "optimizer/plan/planmain.c"
        "optimizer/plan/planner.c"
        "optimizer/plan/setrefs.c"
        "optimizer/plan/subselect.c"
        "optimizer/prep/prepjointree.c"
        "optimizer/prep/prepqual.c"
        "optimizer/prep/preptlist.c"
        "optimizer/prep/prepunion.c"
        "optimizer/util/clauses.c"
        "optimizer/util/joininfo.c"
        "optimizer/util/orclauses.c"
        "optimizer/util/pathnode.c"
        "optimizer/util/placeholder.c"
        "optimizer/util/plancat.c"
        "optimizer/util/predtest.c"
        "optimizer/util/relnode.c"
        "optimizer/util/restrictinfo.c"
        "optimizer/util/tlist.c"
        "optimizer/util/var.c"
        "port/atomics.c"
        "port/dynloader.c"
        "port/pg_sema.c"
        "port/pg_shmem.c"
        "postmaster/autovacuum.c"
        "postmaster/bgworker.c"
        "postmaster/bgwriter.c"
        "postmaster/checkpointer.c"
        "postmaster/fork_process.c"
        "postmaster/pgarch.c"
        "postmaster/pgstat.c"
        "postmaster/postmaster.c"
        "postmaster/startup.c"
        "postmaster/syslogger.c"
        "postmaster/walwriter.c"
        "regex/regcomp.c"
        "regex/regerror.c"
        "regex/regexec.c"
        "regex/regfree.c"
        "regex/regprefix.c"
        "regex/regexport.c"
        "replication/logical/decode.c"
        "replication/logical/launcher.c"
        "replication/logical/logical.c"
        "replication/logical/logicalfuncs.c"
        "replication/logical/message.c"
        "replication/logical/origin.c"
        "replication/logical/proto.c"
        "replication/logical/relation.c"
        "replication/logical/reorderbuffer.c"
        "replication/logical/snapbuild.c"
        "replication/logical/tablesync.c"
        "replication/logical/worker.c"
        "replication/walsender.c"
        "replication/walreceiverfuncs.c"
        "replication/walreceiver.c"
        "replication/basebackup.c"
        "replication/repl_gram.c"
        "replication/slot.c"
        "replication/slotfuncs.c"
        "replication/syncrep.c"
        "replication/syncrep_gram.c"
        "rewrite/rewriteRemove.c"
        "rewrite/rewriteDefine.c"
        "rewrite/rewriteHandler.c"
        "rewrite/rewriteManip.c"
        "rewrite/rewriteSupport.c"
        "rewrite/rowsecurity.c"
        "statistics/extended_stats.c"
        "statistics/dependencies.c"
        "statistics/mvdistinct.c"
        "storage/buffer/buf_table.c"
        "storage/buffer/buf_init.c"
        "storage/buffer/bufmgr.c"
        "storage/buffer/freelist.c"
        "storage/buffer/localbuf.c"
        "storage/file/fd.c"
        "storage/file/buffile.c"
        "storage/file/copydir.c"
        "storage/file/reinit.c"
        "storage/freespace/freespace.c"
        "storage/freespace/fsmpage.c"
        "storage/freespace/indexfsm.c"
        "storage/ipc/dsm_impl.c"
        "storage/ipc/dsm.c"
        "storage/ipc/ipc.c"
        "storage/ipc/ipci.c"
        "storage/ipc/latch.c"
        "storage/ipc/pmsignal.c"
        "storage/ipc/procarray.c"
        "storage/ipc/procsignal.c"
        "storage/ipc/shmem.c"
        "storage/ipc/shmqueue.c"
        "storage/ipc/shm_mq.c"
        "storage/ipc/shm_toc.c"
        "storage/ipc/sinval.c"
        "storage/ipc/sinvaladt.c"
        "storage/ipc/standby.c"
        "storage/large_object/inv_api.c"
        "storage/lmgr/lmgr.c"
        "storage/lmgr/lock.c"
        "storage/lmgr/proc.c"
        "storage/lmgr/deadlock.c"
        "storage/lmgr/lwlock.c"
        "storage/lmgr/lwlocknames.c"
        "storage/lmgr/spin.c"
        "storage/lmgr/s_lock.c"
        "storage/lmgr/predicate.c"
        "storage/lmgr/condition_variable.c"
        "storage/page/bufpage.c"
        "storage/page/checksum.c"
        "storage/page/itemptr.c"
        "storage/smgr/md.c"
        "storage/smgr/smgr.c"
        "storage/smgr/smgrtype.c"
        "tcop/dest.c"
        "tcop/fastpath.c"
        "tcop/postgres.c"
        "tcop/pquery.c"
        "tcop/utility.c"
        "tsearch/ts_locale.c"
        "tsearch/ts_parse.c"
        "tsearch/wparser.c"
        "tsearch/wparser_def.c"
        "tsearch/dict.c"
        "tsearch/dict_simple.c"
        "tsearch/dict_synonym.c"
        "tsearch/dict_thesaurus.c"
        "tsearch/dict_ispell.c"
        "tsearch/regis.c"
        "tsearch/spell.c"
        "tsearch/to_tsany.c"
        "tsearch/ts_selfuncs.c"
        "tsearch/ts_typanalyze.c"
        "tsearch/ts_utils.c"
        "utils/adt/acl.c"
        "utils/adt/amutils.c"
        "utils/adt/arrayfuncs.c"
        "utils/adt/array_expanded.c"
        "utils/adt/array_selfuncs.c"
        "utils/adt/array_typanalyze.c"
        "utils/adt/array_userfuncs.c"
        "utils/adt/arrayutils.c"
        "utils/adt/ascii.c"
        "utils/adt/bool.c"
        "utils/adt/cash.c"
        "utils/adt/char.c"
        "utils/adt/date.c"
        "utils/adt/datetime.c"
        "utils/adt/datum.c"
        "utils/adt/dbsize.c"
        "utils/adt/domains.c"
        "utils/adt/encode.c"
        "utils/adt/enum.c"
        "utils/adt/expandeddatum.c"
        "utils/adt/float.c"
        "utils/adt/format_type.c"
        "utils/adt/formatting.c"
        "utils/adt/genfile.c"
        "utils/adt/geo_ops.c"
        "utils/adt/geo_selfuncs.c"
        "utils/adt/geo_spgist.c"
        "utils/adt/inet_cidr_ntop.c"
        "utils/adt/inet_net_pton.c"
        "utils/adt/int.c"
        "utils/adt/int8.c"
        "utils/adt/json.c"
        "utils/adt/jsonb.c"
        "utils/adt/jsonb_gin.c"
        "utils/adt/jsonb_op.c"
        "utils/adt/jsonb_util.c"
        "utils/adt/jsonfuncs.c"
        "utils/adt/like.c"
        "utils/adt/lockfuncs.c"
        "utils/adt/mac.c"
        "utils/adt/mac8.c"
        "utils/adt/misc.c"
        "utils/adt/nabstime.c"
        "utils/adt/name.c"
        "utils/adt/network.c"
        "utils/adt/network_gist.c"
        "utils/adt/network_selfuncs.c"
        "utils/adt/network_spgist.c"
        "utils/adt/numeric.c"
        "utils/adt/numutils.c"
        "utils/adt/oid.c"
        "utils/adt/oracle_compat.c"
        "utils/adt/orderedsetaggs.c"
        "utils/adt/pg_locale.c"
        "utils/adt/pg_lsn.c"
        "utils/adt/pg_upgrade_support.c"
        "utils/adt/pgstatfuncs.c"
        "utils/adt/pseudotypes.c"
        "utils/adt/quote.c"
        "utils/adt/rangetypes.c"
        "utils/adt/rangetypes_gist.c"
        "utils/adt/rangetypes_selfuncs.c"
        "utils/adt/rangetypes_spgist.c"
        "utils/adt/rangetypes_typanalyze.c"
        "utils/adt/regexp.c"
        "utils/adt/regproc.c"
        "utils/adt/ri_triggers.c"
        "utils/adt/rowtypes.c"
        "utils/adt/ruleutils.c"
        "utils/adt/selfuncs.c"
        "utils/adt/tid.c"
        "utils/adt/timestamp.c"
        "utils/adt/trigfuncs.c"
        "utils/adt/tsginidx.c"
        "utils/adt/tsgistidx.c"
        "utils/adt/tsquery.c"
        "utils/adt/tsquery_cleanup.c"
        "utils/adt/tsquery_gist.c"
        "utils/adt/tsquery_op.c"
        "utils/adt/tsquery_rewrite.c"
        "utils/adt/tsquery_util.c"
        "utils/adt/tsrank.c"
        "utils/adt/tsvector.c"
        "utils/adt/tsvector_op.c"
        "utils/adt/tsvector_parser.c"
        "utils/adt/txid.c"
        "utils/adt/uuid.c"
        "utils/adt/varbit.c"
        "utils/adt/varchar.c"
        "utils/adt/varlena.c"
        "utils/adt/version.c"
        "utils/adt/windowfuncs.c"
        "utils/adt/xid.c"
        "utils/adt/xml.c"
        "utils/cache/attoptcache.c"
        "utils/cache/catcache.c"
        "utils/cache/evtcache.c"
        "utils/cache/inval.c"
        "utils/cache/plancache.c"
        "utils/cache/relcache.c"
        "utils/cache/relmapper.c"
        "utils/cache/relfilenodemap.c"
        "utils/cache/spccache.c"
        "utils/cache/syscache.c"
        "utils/cache/lsyscache.c"
        "utils/cache/typcache.c"
        "utils/cache/ts_cache.c"
        "utils/error/assert.c"
        "utils/error/elog.c"
        "utils/fmgr/dfmgr.c"
        "utils/fmgr/fmgr.c"
        "utils/fmgr/funcapi.c"
        "utils/hash/dynahash.c"
        "utils/hash/hashfn.c"
        "utils/hash/pg_crc.c"
        "utils/init/globals.c"
        "utils/init/miscinit.c"
        "utils/init/postinit.c"
        "utils/mb/encnames.c"
        "utils/mb/conv.c"
        "utils/mb/mbutils.c"
        "utils/mb/wchar.c"
        "utils/mb/wstrcmp.c"
        "utils/mb/wstrncmp.c"
        "utils/misc/backend_random.c"
        "utils/misc/guc.c"
        "utils/misc/help_config.c"
        "utils/misc/pg_config.c"
        "utils/misc/pg_controldata.c"
        "utils/misc/pg_rusage.c"
        "utils/misc/ps_status.c"
        "utils/misc/queryenvironment.c"
        "utils/misc/rls.c"
        "utils/misc/sampling.c"
        "utils/misc/superuser.c"
        "utils/misc/timeout.c"
        "utils/misc/tzparser.c"
        "utils/mmgr/aset.c"
        "utils/mmgr/dsa.c"
        "utils/mmgr/freepage.c"
        "utils/mmgr/mcxt.c"
        "utils/mmgr/memdebug.c"
        "utils/mmgr/portalmem.c"
        "utils/mmgr/slab.c"
        "utils/resowner/resowner.c"
        "utils/sort/logtape.c"
        "utils/sort/sortsupport.c"
        "utils/sort/tuplesort.c"
        "utils/sort/tuplestore.c"
        "utils/time/combocid.c"
        "utils/time/tqual.c"
        "utils/time/snapmgr.c"
        "utils/fmgrtab.c"
        "timezone/localtime.c"
        "timezone/strftime.c"
        "timezone/pgtz.c"
        )

add_executable(test_postgres ${pgbackend_src})
target_link_libraries(test_postgres  pgport_srv pgcommon_srv pthread  rt crypt dl m)